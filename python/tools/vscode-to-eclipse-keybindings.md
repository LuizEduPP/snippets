---
tags: ["python", "tools", "vscode", "eclipse", "keybindings"]
---
# VS Code Keybindings → Eclipse

Reads a `.csv` exported from Eclipse and a `keybindings.json` from VS Code, then generates an `.epf` preferences file with keybindings automatically mapped between the two editors.

## Dependencies

```bash
pip install pandas
```

## Usage

```python
converter_keys(
    csv_path="eclipse_keys.csv",
    vscode_path="keybindings.json",
    output_path="output.epf"
)
```

## How to export the input files

- **Eclipse:** `Window → Preferences → General → Keys → Export CSV`
- **VS Code:** `Ctrl+Shift+P` → `Open Keyboard Shortcuts (JSON)`

## Code

```python
import pandas as pd
import json
import re

def normalize(s):
    if not isinstance(s, str):
        return ''
    return s.lower().replace('_', '').replace('.', '').replace(' ', '')

def read_vscode_keys(vscode_path):
    with open(vscode_path, encoding="utf-8") as f:
        lines = f.readlines()
        json_start = None
        for idx, line in enumerate(lines):
            if line.strip().startswith('['):
                json_start = idx
                break
        return json.loads("".join(lines[json_start:]))

def build_vscode_map(vscode_keys):
    m = {}
    for k in vscode_keys:
        cmd = k.get("command")
        key = k.get("key")
        if cmd and key and cmd not in m:
            m[normalize(cmd)] = key.upper().replace("CMD", "CTRL")
    return m

def map_command(eclipse_cmd, vscode_map):
    candidates = []
    norm = normalize(eclipse_cmd)
    for vcmd in vscode_map:
        if any(part in vcmd for part in re.split(r'[.\-_]', norm)):
            candidates.append(vcmd)
    if not candidates:
        for kw in ['copy', 'paste', 'cut', 'undo', 'redo', 'selectall',
                   'find', 'replace', 'comment', 'rename', 'format', 'save']:
            if kw in norm:
                candidates += [v for v in vscode_map if kw in v]
    if candidates:
        candidates.sort(key=lambda x: (-len(x), x))
        return vscode_map[candidates[0]]
    return None

def converter_keys(csv_path, vscode_path, output_path):
    df = pd.read_csv(csv_path, encoding="ISO-8859-1")
    vscode_map = build_vscode_map(read_vscode_keys(vscode_path))

    rows = []
    for _, row in df.iterrows():
        eclipse_cmd = str(row.iloc[-1])
        eclipse_key = str(row.iloc[2])
        if eclipse_cmd == 'nan':
            continue
        new_key = map_command(eclipse_cmd, vscode_map) or eclipse_key
        if pd.notnull(new_key) and pd.notnull(eclipse_cmd):
            rows.append(
                f"/instance/org.eclipse.ui.workbench/org.eclipse.ui.commands"
                f"/{eclipse_cmd}/{new_key.upper().replace(' ', '')}"
            )

    content = [
        "# Eclipse Preferences",
        "/instance/org.eclipse.ui.workbench/org.eclipse.ui.commands/state=false",
        "file_export_version=3.0",
    ] + rows

    with open(output_path, "w", encoding="utf-8") as f:
        f.write('\n'.join(content))
```

## Import into Eclipse

`File → Import → General → Preferences` → select the generated `.epf` file.
