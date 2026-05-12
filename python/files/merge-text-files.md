---
tags: ["python", "files", "text", "merge"]
---
# Merge and Deduplicate Text Files (Python)

Concatenates multiple text or Markdown files into one, with an optional deduplication pass that removes repeated lines while preserving order.

## Dependencies

No external dependencies — uses Python standard library only.

## Code

### Simple concatenation (preserves duplicates)

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

---

### Merge with deduplication (unique lines, order preserved)

```python
from pathlib import Path
from collections import OrderedDict

files = [
    "notes1.md",
    "notes2.md",
    "notes3.md",
]
output = "merged_unique.md"

seen = OrderedDict()

for path in files:
    for line in Path(path).read_text(encoding="utf-8").splitlines():
        stripped = line.strip()
        if stripped:
            seen[stripped] = None

Path(output).write_text("\n".join(seen.keys()), encoding="utf-8")
print(f"Written {len(seen)} unique lines → {output}")
```

---

### Merge all .md files in a folder (sorted)

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
