---
tags: ["python", "web-api", "iconify", "automation"]
---
# List Collection Icons (Iconify API)

Extracts all available icon names from a single online Iconify collection endpoint, combining both categorized and uncategorized sets automatically into a flat list.

## 🛠️ How it works under the hood

1. **`api.iconify.design`**: Queries the official open repository endpoint.
2. **`categories` dictionary**: Iconify packs some icons inside rigid string categories, and dumps the rest into an `"uncategorized"` array. This script loops through both logic trees and flattens them cleanly.

---

## 🚀 Usage Guide

```python
import requests

def get_collection_icons(prefix: str) -> list:
 url = f"https://api.iconify.design/collection?prefix={prefix}"
 response = requests.get(url)
 
 if response.status_code != 200:
 return []
 
 data = response.json()
 
 uncategorized = data.get("uncategorized", [])
 categories = data.get("categories", {})
 
 all_icons = list(uncategorized)
 for category_icons in categories.values():
 all_icons.extend(category_icons)
 
 return all_icons

if __name__ == "__main__":
 icons = get_collection_icons("mdi")
 print(f"✅ Found {len(icons)} native icons inside the 'mdi' block.")
 # print(icons[:5])
```
