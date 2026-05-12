---
tags: ["shell-linux", "files", "find", "hidden"]
---
# Move Hidden Files and Folders

Moves all contents of a directory — including dotfiles and hidden folders — to another location. The standard `mv /src/*` glob misses hidden entries; you need to include `.*` explicitly.

Paste and run directly in the terminal — no file needed.

## Command

Replace `/source/` and `/destination/` with your paths.

```bash
mv /source/* /source/.* /destination/
```

> This will also try to move `.` and `..` — bash will show harmless "cannot move" warnings for those two entries, which can be safely ignored.

### Safer alternative (avoids the `.` / `..` warnings)

```bash
find /source/ -maxdepth 1 -mindepth 1 -exec mv {} /destination/ \;
```

### List hidden files first to confirm what will be moved

```bash
ls -la /source/
```
