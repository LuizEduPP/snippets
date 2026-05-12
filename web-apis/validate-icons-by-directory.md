---
tags: ["python", "web-api", "iconify", "automation", "files"]
---
# Validate Iconify Icons Across Source Files

Scans a directory tree for `icon="..."` attributes in frontend components and checks each icon name against the Iconify API to find broken or missing references.

## 🛠️ How it works under the hood

1. **`os.walk()` + `re.compile()`**: Walks through every `.js`, `.jsx`, `.ts`, and `.tsx` file in the target directory. A regex pattern (`icon=["']([^"']+)["']`) captures the icon name from each matching line and adds it to a set, so duplicates are only checked once.
2. **Iconify API endpoint**: Each icon name has the format `prefix:name` (e.g., `mdi:home`). The script constructs the URL `https://api.iconify.design/{prefix}.json?icons={name}` and sends a GET request. If the JSON response contains the key `not_found`, the icon does not exist in that collection.
3. **Error handling**: Network timeouts and connection errors are caught per icon so one failure does not stop the rest of the batch.

---

## 🚀 Usage Guide

### 1. Install dependencies
```bash
pip install requests
```

### 2. Run the validation script
```python
import os
import re
import sys
import requests

def find_icons_in_files(base_path: str) -> list[str]:
    """Scan all JS/TS component files and collect unique icon attribute values."""
    pattern = re.compile(r'icon=["\']([^"\']+)["\']')
    found = set()

    for root, dirs, files in os.walk(base_path):
        for file in files:
            if file.endswith(('.js', '.jsx', '.ts', '.tsx')):
                with open(os.path.join(root, file), 'r', encoding='utf-8', errors='ignore') as f:
                    for line in f:
                        found.update(pattern.findall(line))

    return sorted(found)

def validate_icons(icon_list: list[str]) -> tuple[list, list]:
    """Check each icon against the Iconify API. Returns (valid, invalid) lists."""
    valid, invalid = [], []

    for icon in icon_list:
        if ':' not in icon:
            continue  # skip non-prefixed values
        prefix, name = icon.split(':', 1)
        url = f'https://api.iconify.design/{prefix}.json?icons={name}'

        try:
            r = requests.get(url, timeout=20)
            if 'not_found' in r.text:
                print(f"❌ Invalid: {icon}")
                invalid.append(icon)
            else:
                valid.append(icon)
        except Exception as e:
            print(f'⚠️  Error checking {icon}: {e}')

    return valid, invalid

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python validate-icons-by-directory.py ./src")
        sys.exit(1)

    base = sys.argv[1]
    print(f"Scanning: {base}")

    icons = find_icons_in_files(base)
    print(f"{len(icons)} unique icons found. Validating via Iconify API...")

    valid, invalid = validate_icons(icons)

    print(f"\nResults: {len(valid)} valid, {len(invalid)} invalid")
    if invalid:
        print("Invalid icons:")
        for icon in invalid:
            print(f"  - {icon}")
```

### 3. Run it
Pass the path to your source folder as an argument.
```bash
python validate-icons-by-directory.py ./src/components/
```

Expected output:
```
Scanning: ./src/components/
42 unique icons found. Validating via Iconify API...
❌ Invalid: mdi:nonexistent-icon
❌ Invalid: ph:broken-name

Results: 40 valid, 2 invalid
```
