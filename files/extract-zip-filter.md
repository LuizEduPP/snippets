---
tags: ["python", "files", "zip", "filtering", "automation"]
---
# Extract ZIP and Filter Specific Files (Python)

This collection of Python scripts extracts contents from ZIP archives while letting you actively filter for specific file extensions. It also includes utility functions to calculate the size of your extraction and map out the generated file tree.

It is heavily useful when you download a massive `.zip` release of a project but only want to pull out the `.py` or `.css` code files without extracting hundreds of useless assets or compiled binaries.

## 🛠️ How it works under the hood

1. **`zipfile`**: The built-in Python module handling the low-level decompression logic safely. Using it inside a context manager (`with... as zf`) ensures memory streams are safely closed when finished.
2. **`zf.namelist()`**: Generates an array of every file stored inside the zip *without actually extracting them*. This allows us to filter strings before the heavy lifting happens.
3. **`os.walk()`**: A foundational Linux/OS traversal command. It acts like a crawler, recursively diving into sub-directories to map out every single path.

---

## 🚀 Usage Guide

No external dependencies are required. Just replace the placeholder paths directly in the code logic.

### 1. Extract All (Standard)
The basic baseline extraction. Similar to right-click -> Extract.

```python
from zipfile import ZipFile

zip_path = "/path/to/archive.zip"
extract_dir = "/path/to/output"

with ZipFile(zip_path, "r") as zf:
 zf.extractall(extract_dir)

print(f"✅ Extracted to: {extract_dir}")
```

### 2. Extract Specific Extensions Only (Filtered)
This is where the magic happens. We intercept the stream to only pull what matches the `EXTENSIONS` tuple tuple you defined.

```python
from zipfile import ZipFile

zip_path = "/path/to/archive.zip"
extract_dir = "/path/to/output"
EXTENSIONS = (".py", ".js", ".ts", ".html", ".css")

with ZipFile(zip_path, "r") as zf:
 # Filter the index list before extraction
 targets = [f for f in zf.namelist() if f.endswith(EXTENSIONS)]
 
 # Process only the targets
 for entry in targets:
 zf.extract(entry, extract_dir)
 print(f"Extracted: {entry}")
```

---

## 💡 Advanced Diagnostics

Once extracted, you might want to analyze what was dumped into your folder.

### List all files This uses Python paths relative to the extraction folder to build a clean terminal list.

```python
import os

def list_files(directory):
 result = []
 for root, dirs, files in os.walk(directory):
 for file in files:
 full = os.path.join(root, file)
 # Make the output path look clean based on relative positioning
 result.append(os.path.relpath(full, directory))
 return result

for f in list_files(extract_dir):
 print(f)
```

### Fetch Directory Size and Stats
This function walks the structure, calculating raw byte sizes for the entire directory to flag exactly how heavy the extraction was.

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
print(f"📊 Extraction Stats: {count} files — {size / 1024:.1f} KB")
```
