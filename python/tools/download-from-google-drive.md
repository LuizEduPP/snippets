---
tags: ["python", "tools", "google-drive", "download", "gdown"]
---
# Download Files from Google Drive (Python)

Downloads files from a public Google Drive link using `gdown`, with local caching to skip already-downloaded files. Also includes a PyInstaller-compatible path helper.

## Dependencies

```bash
pip install gdown
```

## Code

### Download a single file (skip if already exists)

```python
import os
import gdown

def download_if_missing(url: str, dest: str) -> None:
    """Downloads a Google Drive file only if not already present."""
    if not os.path.exists(dest):
        print(f"Downloading {dest}...")
        gdown.download(url, dest, quiet=False)
    else:
        print(f"{dest} already exists. Skipping.")
```

### Usage

```python
# Get the file ID from the Drive share link:
# https://drive.google.com/file/d/FILE_ID/view
# Use: https://drive.google.com/uc?id=FILE_ID

download_if_missing(
    url="https://drive.google.com/uc?id=1k2dDQ-Lj0pdneCqgAPItkzD6FZMgAyWn",
    dest="data/clients.csv"
)
```

### Download a full folder

```python
gdown.download_folder(
    url="https://drive.google.com/drive/folders/FOLDER_ID",
    output="data/",
    quiet=False
)
```

---

## PyInstaller-compatible asset path

When bundling with PyInstaller, `open("assets/file.csv")` breaks because the working directory changes. Use this helper instead:

```python
import sys
import os

def get_asset_path(relative_path: str) -> str:
    """Returns absolute path to an asset, works for both script and PyInstaller bundle."""
    if getattr(sys, "frozen", False):
        base = sys._MEIPASS
    else:
        base = os.path.abspath(".")
    return os.path.join(base, relative_path)

# Usage
csv_path = get_asset_path("assets/clients.csv")
```
