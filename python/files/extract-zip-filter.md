---
tags: ["python", "files", "zip"]
---
# Extract ZIP and Filter Files (Python)

Extracts a ZIP archive, optionally filtering by extension, and lists directory contents with stats.

## Dependencies

```bash
pip install pathlib  # built-in on Python 3.4+, no install needed
```

## Code

### Extract all files

```python
from zipfile import ZipFile

zip_path = "/path/to/archive.zip"
extract_dir = "/path/to/output"

with ZipFile(zip_path, "r") as zf:
    zf.extractall(extract_dir)

print(f"Extracted to: {extract_dir}")
```

### Extract only specific extensions

```python
from zipfile import ZipFile

EXTENSIONS = (".py", ".js", ".ts", ".html", ".css")

with ZipFile(zip_path, "r") as zf:
    targets = [f for f in zf.namelist() if f.endswith(EXTENSIONS)]
    for entry in targets:
        zf.extract(entry, extract_dir)
```

### List all files recursively

```python
import os

def list_files(directory):
    result = []
    for root, dirs, files in os.walk(directory):
        for file in files:
            full = os.path.join(root, file)
            result.append(os.path.relpath(full, directory))
    return result

for f in list_files(extract_dir):
    print(f)
```

### Directory stats (file count + total size)

```python
import os

def dir_stats(directory):
    total_files = 0
    total_size = 0
    for root, dirs, files in os.walk(directory):
        total_files += len(files)
        for f in files:
            total_size += os.path.getsize(os.path.join(root, f))
    return total_files, total_size

count, size = dir_stats(extract_dir)
print(f"{count} files — {size / 1024:.1f} KB")
```
