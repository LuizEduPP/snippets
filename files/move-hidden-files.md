---
tags: ["linux", "files", "find", "hidden", "automation"]
---
# Move Hidden Files and Folders 

When you run a standard `mv /source/* /destination/` command, the `*` wildcard ignores hidden files (dotfiles like `.git`, `.env`, `.gitignore`). This causes nasty bugs when trying to copy entire repositories.

This guide lists two approaches to ensuring *all* contents of a directory are moved successfully.

## 🛠️ How it works under the hood

1. **`mv`**: The standard Linux utility for moving files and directories.
2. **`*`**: Instructs bash to grab all visible, normal files inside the source directory.
3. **`.*`**: Instructs bash to specifically grab all hidden items (files and folders starting with a dot).
4. **`find`** (in advanced method): Directly crawls the file system instead of relying on Bash wildcard expansion, grabbing absolute objects systematically.

---

## 🚀 Usage Guide

Replace `/source/` and `/destination/` with your actual system paths.

### 1. The Quick Glob Method
By specifying both `*` and `.*`, you force the shell to move everything.

```bash
mv /source/* /source/.* /destination/
```

> **Warning:** You will see an error saying `cannot move '.' to a subdirectory of itself`. This happens because `.` (current dir) and `..` (parent dir) are caught by the `.*` wildcard. You can safely ignore this harmless warning.

### 2. The Clean Find Method (Recommended)
This approach completely avoids the annoying `.` and `..` glob errors by using `find` to target content inside the folder exactly exactly 1 level deep.

```bash
find /source/ -maxdepth 1 -mindepth 1 -exec mv {} /destination/ \;
```
- `-mindepth 1`: Ignores the actual `/source/` directory itself, targeting only what's inside.
- `-maxdepth 1`: Stops it from traversing subfolders recursively (which `mv` already handles naturally).
- `-exec mv {}`: Runs `mv` targeting the found path.

### 💡 Extra: List before moving
If you're unsure if a directory contains hidden files, check it by using the list all (`-a`) flag.

```bash
ls -la /source/
```
