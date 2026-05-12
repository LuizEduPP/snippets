---
tags: ["shell-linux", "system", "diff", "merge", "git"]
---
# Diff and Merge Tools for Linux

Visual and terminal-based alternatives to WinMerge for comparing and merging files on Linux.

Paste and run directly in the terminal — no file needed.

## GUI tools

### Meld (recommended — GTK, free)

```bash
# Debian/Ubuntu/Zorin
sudo apt install meld

# Arch/Manjaro
sudo pacman -S meld
```

```bash
meld file1.txt file2.txt
meld dir1/ dir2/
```

### KDiff3

```bash
sudo apt install kdiff3
```

### Diffuse

```bash
sudo apt install diffuse
```

### Kompare (KDE)

```bash
sudo apt install kompare
```

---

## Terminal tools

### vimdiff

```bash
vimdiff file1.txt file2.txt
```

> `:diffget` / `:diffput` to merge hunks. `:wqa` to quit all.

### diff + patch

```bash
# Show differences
diff -u old.txt new.txt

# Create patch file
diff -u old.txt new.txt > changes.patch

# Apply patch
patch old.txt < changes.patch
```

### colordiff (colorized diff output)

```bash
sudo apt install colordiff
colordiff file1.txt file2.txt
```
