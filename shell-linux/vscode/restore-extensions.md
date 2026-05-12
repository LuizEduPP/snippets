---
tags: ["shell-linux", "vscode", "extensions", "backup"]
---
# Restore VS Code Extensions

Reinstalls a predefined set of extensions into **VS Code Insiders** from a hardcoded list. Useful after a fresh OS install or when setting up a new machine.

Paste and run directly in the terminal — no file needed.

> To use with stable VS Code, replace `code-insiders` with `code`.

Find any extension ID in its Marketplace URL:  
`https://marketplace.visualstudio.com/items?itemName=<ID>`

## Command

```bash
EXTENSIONS=(
  ms-vscode.js-debug
  ms-vscode.js-debug-companion
  ms-vscode.vscode-js-profile-table
  esbenp.prettier-vscode
  github.copilot
  github.copilot-chat
  codeium.codeium
  redhat.vscode-yaml
  eamodio.gitlens
)

echo "Installing extensions into VS Code Insiders..."

for EXT in "${EXTENSIONS[@]}"; do
  echo "  Installing $EXT"
  code-insiders --install-extension "$EXT" --force
done

echo "Done."
```
