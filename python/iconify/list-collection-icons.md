---
tags: ["python", "iconify", "icons"]
---
# List All Icons in an Iconify Collection

Queries the Iconify API and prints every icon in a collection, grouped by category, with a total count at the end.

## Dependencies

```bash
pip install requests
```

## Usage

Change the `prefix` in the URL to target any collection:

```python
url = "https://api.iconify.design/collection?prefix=mdi"    # Material Design Icons
url = "https://api.iconify.design/collection?prefix=ph"     # Phosphor Icons
url = "https://api.iconify.design/collection?prefix=tabler" # Tabler Icons
url = "https://api.iconify.design/collection?prefix=line-md" # Line MD (default)
```

Browse all available collections at: https://icon-sets.iconify.design

## Code

```python
import requests

url = "https://api.iconify.design/collection?prefix=line-md"

try:
    response = requests.get(url)
    data = response.json()

    categories = data.get("categories", {})
    total = 0

    for category, icons in categories.items():
        print(f"\n Category: {category} ({len(icons)} icons)")
        for icon in icons:
            print(f"  - line-md:{icon}")
            total += 1

    print(f"\n Total icons listed: {total}")

except Exception as e:
    print("Error querying API:", e)
```

## Expected output

```
 Category: Animated (42 icons)
  - line-md:loading-loop
  - line-md:moon-alt-to-sunny-outline-loop-transition
  ...

 Total icons listed: 247
```
