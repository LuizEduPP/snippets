---
tags: ["linux", "files", "jq", "json", "data"]
---
# Extract Keys from JSON using `jq`

This is a fast workflow for extracting, sorting, and combining object keys from a JSON file directly into your terminal. It relies heavily on `jq`, which is the industry standard tool for handling JSON from the command line.

It is extremely useful when inspecting heavy configuration files, reading API responses, or dumping lists of items (like icon collections) to plain `.txt` or `.csv` files.

## 🛠️ How it works under the hood

The magic lies in how `jq` evaluates filters:

1. **`jq -r`**: The `-r` flag tells `jq` to output "raw" text. Without it, string keys would still have double quotes around them (e.g., `"key"`). With it, it simply prints `key`.
2. **`'.icons | keys[]'`**:
 - `.icons`: Targets the top-level property named `icons` in your JSON file.
 - `| keys`: Passes that object into the `keys` function, which extracts all property names into a JSON array.
 - `[]`: Unpacks the array, tossing each key onto a new line, returning a plain list.
3. **`| sort`**: Uses standard bash sorting to organize the keys alphabetically.
4. **`paste -sd, -`** (in the inline variant): `paste` usually merges lines from multiple files file. The `-s` flag tells it to join lines serially from standard input (`-`), divided by a comma delimiter (`-d,`), creating one giant string.

---

## ⚡ Setup / Installation

If you don't have `jq`, you must grab it via your package manager:

```bash
# Ubuntu / Debian
sudo apt install jq

# Fedora
sudo dnf install jq

# Arch Linux / Manjaro
sudo pacman -S jq
```

## 🚀 Usage Guide

### 1. Print keys directly to the terminal
Targets the `icons` object inside `file.json` and outputs all its keys. ```bash
jq -r '.icons | keys[]' file.json | sort
```

### 2. Save the output to a text file
Same as above, but uses `>` to redirect the final sorted output directly into `icons.txt`.

```bash
jq -r '.icons | keys[]' file.json | sort > icons.txt
```

### 3. Create a single comma-separated line (CSV style inline)
If you need to paste these keys into a JavaScript Array or a Python List, this joins them. ```bash
jq -r '.icons | keys[]' file.json | sort | paste -sd, - > icons-inline.txt
```
*Expected Output inside the text file:* `account,account-add,account-alert`

### 4. How many keys are there?
Quickly count the size of an object rather than printing out the keys themselves.

```bash
jq '.icons | length' file.json
```
