---
tags: ["linux", "files", "find", "delete", "time"]
---
# Find and Delete Files Modified by Time

This script utilizes `find` with a precise timestamp filter to either list or delete files that were modified before a specific time limit on the *current day*.

It's highly effective for cleaning up temporary download folders, log files, or massive render dumps where you want to keep only the newest files created after a specific hour.

## 🛠️ How it works under the hood

1. **`find /path`**: Tells Linux to start searching from the defined path.
2. **`-type f`**: Filters the search to strictly return files (ignores directories/links).
3. **`-not -newermt "..."`**: The core logic filter.
   - `-newermt` means "newer than modification time".
   - `$(date +%Y-%m-%d) 11:30`: Automatically fetches today's current date string and appends `11:30` to it.
   - By prefixing `-not`, we invert the rule: it finds files that are *older* (not newer) than 11:30 AM today!
4. **`-exec rm -f {} +`** (on delete action): Replaces `{}` with the found file path. The `+` bundles multiple files in a single background command batch, dramatically speeding up mass deletes.

---

## 🚀 Usage Guide 

### 1. Safety Check (Dry Run List)
Always run this before the delete command to make sure you are targeting the correct files!

```bash
find ~/Downloads -type f -not -newermt "$(date +%Y-%m-%d) 11:30"
```

### 2. Delete the files
This will permanently delete the matched target files.

```bash
find /path/to/folder -type f -not -newermt "$(date +%Y-%m-%d) 11:30" -exec rm -f {} +
```

*(Note: Change `/path/to/folder` to your target directory, such as `.` to target the current folder, and change `11:30` to your desired cutoff time).*

---

## 💡 Advanced: Count old files by extension

If you want an analytical breakdown of what kind of files are going to be purged (or just generally count files in your system matching an extension rule):

```bash
for ext in py js ts html css json xml md txt; do
  count=$(find /path/to/folder -type f -name "*.$ext" | wc -l)
  printf "%-6s: %d\n" "$ext" "$count"
done
```

**Expected terminal output:**
```text
py    : 12
js    : 35
ts    : 15
html  : 20
...
```

Instead of looping, to get a single unified count across multiple extensions extremely fast:
```bash
find /path/to/folder -type f \( \
  -name "*.py" -o -name "*.js" -o -name "*.ts" \
  -o -name "*.html" -o -name "*.css" -o -name "*.json" \
\) | wc -l
```
