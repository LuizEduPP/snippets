---
tags: ["shell-linux", "files", "find", "delete"]
---
# Find and Delete Files Older Than a Time (find)

Uses `find` with a timestamp filter to list or delete files modified before a specific time on the same day. Also includes a file count breakdown by extension.

Paste and run directly in the terminal — no file needed.

## Command

### List files modified before 11:30 today (dry run)

```bash
find ~/Downloads -type f -not -newermt "$(date +%Y-%m-%d) 11:30"
```

### Delete files modified before 11:30 today

```bash
find /path/to/folder -type f -not -newermt "$(date +%Y-%m-%d) 11:30" -exec rm -f {} +
```

> Change `11:30` to any `HH:MM` value. Runs in the current directory when using `.` as path.

### Delete in current directory

```bash
find . -type f -not -newermt "$(date +%Y-%m-%d) 11:30" -exec rm -f {} +
```

---

## Count files by extension

```bash
for ext in py js ts html css json xml md txt; do
  count=$(find /path/to/folder -type f -name "*.$ext" | wc -l)
  printf "%-6s: %d\n" "$ext" "$count"
done
```

Example output:

```
py    : 12
js    : 35
ts    : 15
html  : 20
css   : 18
json  : 11
xml   : 6
md    : 5
txt   : 30
```

### Count all files matching specific extensions in one pass

```bash
find /path/to/folder -type f \( \
  -name "*.py" -o -name "*.js" -o -name "*.ts" \
  -o -name "*.html" -o -name "*.css" -o -name "*.json" \
\) | wc -l
```
