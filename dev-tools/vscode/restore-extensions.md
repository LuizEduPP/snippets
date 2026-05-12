---
tags: ["bash", "vscode", "extensions", "backup", "system"]
---
# Restore VS Code Extensions

Automates the installation of a predefined list of extensions using the VS Code CLI. Useful for setting up a new environment.

## 🛠️ How it works under the hood

1. **`code --install-extension` command**: The VS Code CLI provides flags to manage extensions from the terminal. The script iterates through a Bash array containing extension IDs and requests them from the Microsoft Marketplace. The `--force` flag ensures updates if an outdated version is present.

---

## 🚀 Usage Guide

### 1. Find Extension IDs
Locate the ID in the Marketplace URL:
`https://marketplace.visualstudio.com/items?itemName=<ID>`

### 2. Run Restoration Script
Modify the `EXTENSIONS` array and execute the script.
```bash
# Define your extension list
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
  
  # Use 'code' instead of 'code-insiders' for stable releases
  code-insiders --install-extension "$EXT" --force
done

echo "Done."
```
