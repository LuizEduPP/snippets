---
tags: ["python", "iconify", "icons", "validation"]
---
# Validate Iconify Icons in a JS/TS Project

Scans a directory for `.js`, `.jsx`, `.ts`, and `.tsx` files, extracts all `icon="..."` attribute values, and validates each one via the Iconify API. Reports valid and invalid icons.

## Dependencies

```bash
pip install requests
```

## Usage

```bash
python validate-icons-by-directory.py ./src
```

## Code

```python
import os
import re
import sys
import requests

def find_icons_in_files(base_path):
    pattern = re.compile(r'icon=["\']([^"\']+)["\']')
    found = set()

    for root, dirs, files in os.walk(base_path):
        for file in files:
            if file.endswith(('.js', '.jsx', '.ts', '.tsx')):
                with open(os.path.join(root, file), 'r', encoding='utf-8', errors='ignore') as f:
                    for line in f:
                        matches = pattern.findall(line)
                        found.update(matches)
    return sorted(found)

def validate_icons(icon_list):
    valid, invalid = [], []
    for icon in icon_list:
        if ':' not in icon:
            continue
        prefix, name = icon.split(':', 1)
        url = f'https://api.iconify.design/{prefix}.json?icons={name}'
        try:
            r = requests.get(url, timeout=20)
            if 'not_found' in r.text:
                print(f"Invalid: {icon}")
                invalid.append(icon)
            else:
                valid.append(icon)
        except Exception as e:
            print(f'Error validating {icon}: {e}')
    return valid, invalid

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python validate-icons-by-directory.py <path>")
        sys.exit(1)

    base = sys.argv[1]
    print(f"Scanning: {base}")
    icons = find_icons_in_files(base)
    print(f"{len(icons)} icons found.")

    print("Validating via Iconify API...")
    valid, invalid = validate_icons(icons)

    print("\nValid icons:")
    for icon in valid:
        print(" -", icon)

    print("\nInvalid icons:")
    for icon in invalid:
        print(" -", icon)
```

## Expected file format

```jsx
<Icon icon="mdi:home" />
<Icon icon="ph:user-bold" />
<Icon icon="line-md:loading-loop" />
```
