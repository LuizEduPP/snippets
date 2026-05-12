---
tags: ["bash", "vscode", "vscodium", "install", "linux"]
---
# Install VSCodium

Installs VSCodium, an open-source build of VS Code that removes Microsoft branding and telemetry tracking.

## 🛠️ How it works under the hood

1. **Package repositories**: The installation commands add the official GitLab-hosted package repository for VSCodium to the OS package manager. This allows `apt` or `pacman` to fetch the binaries and handle updates like any standard system application.

---

## 🚀 Usage Guide

### 1. Install via Package Managers

**Linux — Debian/Ubuntu (APT)**
```bash
# Add GPG key
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
  | gpg --dearmor \
  | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg

# Add repository
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
  | sudo tee /etc/apt/sources.list.d/vscodium.list

# Install
sudo apt update && sudo apt install codium
```

**Linux — Arch/Manjaro (AUR)**
```bash
yay -S vscodium-bin
# or
pamac install vscodium-bin
```

**macOS — Homebrew**
```bash
brew install --cask vscodium
```

### 2. General Usage Notes
- The default command-line executable name is `codium`, not `code`.
- Extensions are fetched from the Open VSX Registry. Proprietary extensions that require Microsoft signing (like Live Share) are incompatible.
- You can copy your `settings.json` and `keybindings.json` from a previous VS Code installation to retain your environment.
