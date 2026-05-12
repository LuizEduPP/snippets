---
tags: ["python", "files", "text", "merge", "automation"]
---
# Merge and Deduplicate Text Files (Python)

This guide provides three lightweight Python scripts to concatenate multiple text or Markdown files into a single master document. One variant even includes an intelligent deduplication pass that automatically strips out repeated lines while preserving the document's original reading order.

These scripts are highly useful for joining fragmented logs, organizing chapter-based Markdown books, or compiling code chunks.

## 🛠️ How it works under the hood

1. **`Pathlib`**: A modern Python standard library used here to safely read and write bytes without getting tangled in complex directory string concats.
2. **`OrderedDict`** (in deduplication): A specialized dictionary from the `collections` module. Normal sets (`set()`) destroy the order of your items when removing duplicates, but `OrderedDict` remembers the exact sequence in which it first saw a line of text, guaranteeing the resulting file reads from top to bottom.

---

## 🚀 Usage Guide

You can run these scripts via `python3 script.py`. No external dependencies (`pip` packages) are required!

### 1. Simple Concatenation (Preserves exact content)
A rapid byte-by-byte merge of specified files. Super fast.

```python
from pathlib import Path

files = [
 "chapter1.md",
 "chapter2.md",
 "chapter3.md",
]
output = "merged.md"

with open(output, "wb") as out:
 for path in files:
 out.write(Path(path).read_bytes())

print(f"Merged {len(files)} files → {output}")
```

### 2. Merge with Smart Deduplication (Unique lines only)
If your files share redundant data, this extracts lines exactly once.

```python
from pathlib import Path
from collections import OrderedDict

files = [
 "notes1.md",
 "notes2.md",
 "notes3.md",
]
output = "merged_unique.md"

# Automatically drops duplicates while remembering the reading order
seen = OrderedDict()

for path in files:
 for line in Path(path).read_text(encoding="utf-8").splitlines():
 stripped = line.strip()
 if stripped: # ignores completely empty lines
 seen[stripped] = None

# Recompile the unique lines together
Path(output).write_text("\n".join(seen.keys()), encoding="utf-8")
print(f"Written {len(seen)} unique lines → {output}")
```

### 3. Folder Scan (Merge all `.md` files automatically)
Instead of typing the array manually, point this at a directory and it will merge everything inside dynamically, injecting the filename as a header!

```python
from pathlib import Path

folder = Path("notes/")
output = Path("all_notes.md")

with output.open("w", encoding="utf-8") as out:
 for md_file in sorted(folder.glob("*.md")):
 out.write(f"\n\n# {md_file.stem}\n\n")
 out.write(md_file.read_text(encoding="utf-8"))

print(f"Merged {len(list(folder.glob('*.md')))} files → {output}")
```
