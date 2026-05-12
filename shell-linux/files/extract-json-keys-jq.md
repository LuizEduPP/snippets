---
tags: ["shell-linux", "files", "jq", "json"]
---
# Extract Keys from JSON with jq

Uses `jq` to list keys from a JSON object — useful for inspecting icon collections, config files, and API responses.

Paste and run directly in the terminal — no file needed.

## Install

```bash
# Arch/Manjaro
sudo pacman -S jq

# Debian/Ubuntu
sudo apt install jq

# Fedora
sudo dnf install jq
```

## Command

### List all keys from an object field

```bash
jq -r '.icons | keys[]' file.json | sort
```

### List alias keys

```bash
jq -r '.aliases | keys[]' file.json | sort
```

### Save keys to a text file

```bash
jq -r '.icons | keys[]' file.json | sort > icons.txt
jq -r '.aliases | keys[]' file.json | sort > aliases.txt
```

### Export keys as a single comma-separated line

```bash
jq -r '.icons | keys[]' file.json | sort | paste -sd, - > icons-inline.txt
```

> Output: `account,account-add,account-alert,...`

### Merge keys and aliases into a CSV

```bash
echo "icon,alias" > icons-with-aliases.csv
paste -d, icons.txt aliases.txt >> icons-with-aliases.csv
```

### Count total keys

```bash
jq '.icons | keys | length' file.json
```
