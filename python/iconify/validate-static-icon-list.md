---
tags: ["python", "iconify", "icons", "validation"]
---
# Validate a Static Iconify Icon List

Validates a hardcoded list of `line-md` icons against the Iconify API and prints which ones were not found.

Useful for quickly checking whether icons used in a project still exist in the collection.

## Dependencies

```bash
pip install requests
```

## Usage

Edit the `icons` list in the code and run:

```bash
python validate-static-icon-list.py
```

## Code

```python
import requests

icons = [
    "content-save", "palette-twotone", "tune-vertical", "api", "information",
    "wrench", "alert-circle", "refresh", "delete-forever", "sleep", "close-circle",
    "clipboard-list-twotone", "plus", "filter-alt", "search", "arrow-up", "calendar",
    "alert", "pencil", "delete", "brain-alt", "trash", "loading", "progress-upload",
    "target", "star", "send", "robot", "content-copy", "history", "refresh-circle",
    "check-all", "confirm-circle", "view-column-plus", "tray-arrow-down", "repeat",
    "trophy", "check-list-3", "lightbulb", "hand-wave", "arrow-right", "lightning",
    "chevron-right", "gift", "meditation", "target-plus", "plus-circle", "minus-circle"
]

invalid = []

for icon in icons:
    url = f"https://api.iconify.design/line-md.json?icons={icon}"
    res = requests.get(url)
    data = res.json()
    if "not_found" in data and icon in data["not_found"]:
        invalid.append(icon)

print("Invalid icons:", invalid)
```

## Expected output

```
Invalid icons: ['brain-alt', 'check-list-3', 'lightning']
```

> To validate a different collection, replace `line-md` in the URL with the desired prefix (e.g., `mdi`, `ph`, `tabler`).
