---
tags: ["shell-linux", "files", "zip", "unzip"]
---
# Extract ZIP Without Subfolders

Extracts all files from a ZIP archive into a flat output directory, stripping the original folder structure.

Paste and run directly in the terminal — no file needed.

## Command

Replace `archive.zip` with your file and `output/` with your target directory.

### Using `unzip -j` (fastest)

```bash
unzip -j archive.zip -d output/
```

The `-j` flag ("junk paths") discards all directory info and dumps every file into `output/`.

### Using `find` (when you need conflict control)

```bash
unzip archive.zip -d _tmp && find _tmp -type f -exec mv -n {} output/ \; && rm -rf _tmp
```

> `-n` (no-clobber) skips files that already exist in `output/`. Remove it to overwrite.
