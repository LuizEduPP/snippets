---
tags: ["shell-linux", "vscode", "vscodium", "install"]
---
# Install VSCodium (Open-Source VS Code, No Telemetry)

Installs VSCodium — a community build of VS Code with Microsoft branding and telemetry removed.

Paste and run directly in the terminal — no file needed.

## Command

### Linux — Debian/Ubuntu (official repo)

```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
  | gpg --dearmor \
  | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg

echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
  | sudo tee /etc/apt/sources.list.d/vscodium.list

sudo apt update && sudo apt install codium
```

### Linux — Arch/Manjaro (AUR)

```bash
yay -S vscodium-bin
# or
pamac install vscodium-bin
```

### macOS — Homebrew

```bash
brew install --cask vscodium
```

---

## Notes

- The binary is named `codium`, not `code`.
- Extensions are installed from the **Open VSX Registry** instead of the Microsoft Marketplace. Install marketplace extensions manually via `.vsix` files if needed.
- Settings and keybindings from VS Code can be copied directly (same JSON format).
- VS Code extensions that require Microsoft-signed binaries (Live Share, Pylance) may not work in VSCodium.
