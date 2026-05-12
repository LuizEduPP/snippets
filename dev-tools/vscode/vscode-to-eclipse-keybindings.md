---
tags: ["python", "vscode", "eclipse", "keybindings", "migration"]
---
# VS Code Keybindings → Eclipse

Reads an exported VS Code `keybindings.json` and an Eclipse-exported `.csv` file to produce an `.epf` preferences file that remaps Eclipse shortcuts to match your VS Code muscle memory.

## 🛠️ How it works under the hood

1. **Format mismatch**: VS Code stores bindings as a JSON array (command → key), while Eclipse uses a flat Java namespace format inside `.epf` files (e.g., `org.eclipse.ui.commands/org.eclipse.ui.edit.copy=CTRL+C`). The script bridges this gap by parsing the JSON and constructing matching `.epf` lines.
2. **`normalize()`**: Strips dots, underscores, and spaces from command names before comparing. This lets `org.eclipse.ui.edit.copy` match against `editor.action.clipboardCopyAction` without an exact string lookup.
3. **`map_command()`**: Splits an Eclipse command name into its meaningful segments and checks each one against the normalized VS Code command map. Falls back to common keyword matches (`copy`, `paste`, `undo`, etc.) if no specific candidate is found.
4. **`pandas.read_csv()`**: Parses the Eclipse `.csv` export. Eclipse uses ISO-8859-1 encoding on some systems, so the encoding parameter is set accordingly.
5. **`.epf` output**: Eclipse preference files are plain text. Each line follows the pattern `/instance/<plugin>/command=KEY`. The script builds these lines from matched pairs and adds a header that Eclipse requires to accept the import.

---

## 🚀 Usage Guide

### 1. Export settings from both IDEs

From **Eclipse**: `Window → Preferences → General → Keys → Export CSV`

From **VS Code**: `Ctrl+Shift+P` → `Open Keyboard Shortcuts (JSON)` → save the file

### 2. Install dependencies
```bash
pip install pandas
```

### 3. Run the translation script
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
        json_start = next(i for i, l in enumerate(lines) if l.strip().startswith('['))
        return json.loads("".join(lines[json_start:]))

def build_vscode_map(vscode_keys):
    m = {}
    for k in vscode_keys:
        cmd, key = k.get("command"), k.get("key")
        if cmd and key and cmd not in m:
            m[normalize(cmd)] = key.upper().replace("CMD", "CTRL")
    return m

def map_command(eclipse_cmd, vscode_map):
    norm = normalize(eclipse_cmd)
    candidates = [v for v in vscode_map if any(p in v for p in re.split(r'[.\-_]', norm))]
    if not candidates:
        candidates = [v for v in vscode_map
                      for kw in ['copy','paste','cut','undo','redo','find','replace','comment','save']
                      if kw in norm and kw in v]
    return vscode_map[sorted(candidates, key=lambda x: (-len(x), x))[0]] if candidates else None

def convert_keys(csv_path, vscode_path, output_path):
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

    lines = [
        "# Eclipse Preferences",
        "/instance/org.eclipse.ui.workbench/org.eclipse.ui.commands/state=false",
        "file_export_version=3.0",
    ] + rows

    with open(output_path, "w", encoding="utf-8") as f:
        f.write('\n'.join(lines))
    print(f"Written: {output_path} ({len(rows)} bindings mapped)")

convert_keys(
    csv_path="eclipse_keys.csv",
    vscode_path="keybindings.json",
    output_path="output.epf"
)
```

### 4. Import into Eclipse
Go to `File → Import → General → Preferences` and select the generated `output.epf`.

Eclipse will apply the new bindings. Restart may be required for all shortcuts to take effect.
