---
tags: ["python", "web-api", "iconify", "automation"]
---
# Validate a Static Iconify Icon List

A fast script to validate a hardcoded Python array of Iconify names against their live servers to verify if developers have deprecated or renamed any assets in the specific `line-md` collection.

## 🛠️ How it works under the hood

1. **API Endpoints**: Iconify provides targeted JSON endpoints via `https://api.iconify.design/{prefix}.json?icons={name}` that respond instantly.
2. **`data["not_found"]`**: Rather than checking HTTP 404, we must parse the returned JSON document, because Iconify returns 200 OK often but appends unreachable icons to a `"not_found"` JSON bucket schema.

---

## ⚡ Setup / Installation

Install the standard HTTP fetcher:
```bash
pip install requests
```

---

## 🚀 Usage Guide

Append or swap out elements in the `icons` array as needed:

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

print("📡 Validating static icons...")

for icon in icons:
    # Change 'line-md' below to your targeted icon prefix (e.g. mdi, tabler, etc.)
    url = f"https://api.iconify.design/line-md.json?icons={icon}"
    
    res = requests.get(url)
    data = res.json()
    
    # Safely look for the not_found block to verify validity
    if "not_found" in data and icon in data["not_found"]:
        invalid.append(icon)

if invalid:
    print(f"❌ Found {len(invalid)} broken icons: {invalid}")
else:
    print("✅ All icons are valid and reachable!")
```
