---
tags: ["bash", "git", "hook", "commit", "convention"]
---
# Auto-Format Git Commit Messages

Applies an absolute Git hook locally executing bash limits designed to enforce explicit Angular convention arrays on all commit strings inherently. ## 🛠️ How it works under the hood

1. **`commit-msg` boundary execution**: Before Git finalizes local tree nodes cleanly, it parses `.git/hooks`. This script executes directly against the temporary file `$1`, validating regex blocks. If it faults, standard STDERR limits halt execution immediately.

---

## 🚀 Usage Guide

### 1. View Assigned File
Position directly inside local `.git` structures.
```bash
# Navigate cd.git/hooks/
```

### 2. Lock Hook Script Down
Create and make the execution file executable. 
```bash
cat << 'EOF_INTERNAL' > commit-msg
#!/bin/bash
# commit-msg - Validate commit message structure cleanly.

msg_file=$1
msg_content=$(cat "$msg_file")

# Standard regex limits blocking bad strings
if ! echo "$msg_content" | grep -Pq '^(feat|fix|docs|style|refactor|test|chore|build|ci|revert)(\([a-z0-9\-]+\))?:.+$'; then
 echo "ERROR: Invalid commit. "
 echo "Use: type(scope): message limits"
 exit 1
fi
EOF_INTERNAL

# Expose executable limits chmod +x commit-msg
```
