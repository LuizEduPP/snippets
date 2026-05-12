---
tags: ["shell-linux", "files", "git", "hook", "commit"]
---
# Auto-populate Git Commit Message (Hook)

A `prepare-commit-msg` hook that pre-fills the commit message with the current branch name and a summary of staged changes. The message is still editable before you confirm.

Paste and run directly in the terminal — no file needed.

## Setup

Create the hook file inside your repository:

```bash
cat > .git/hooks/prepare-commit-msg << 'EOF'
#!/bin/bash

DEFAULT_MSG="Updates on branch $(git branch --show-current)"
CUSTOM_MSG=$(cat "$1")

FINAL_MSG="$DEFAULT_MSG"
if [ -n "$CUSTOM_MSG" ]; then
    FINAL_MSG+=$'\n'"$CUSTOM_MSG"
fi

DIFF=$(git diff --cached --stat)
if [ -n "$DIFF" ]; then
    FINAL_MSG+=$'\n\nChanged files:\n'"$DIFF"
fi

echo -e "$FINAL_MSG" > "$1"
EOF
chmod +x .git/hooks/prepare-commit-msg
```

## Example output

Running `git commit` opens the editor pre-filled with:

```
Updates on branch main

Changed files:
 src/pages/Clients/ClientsList.tsx | 19 +++++---
 src/api/clients.ts                |  4 +-
```

> Edit or clear the message before saving. The hook only populates the editor — it does not bypass the commit.
