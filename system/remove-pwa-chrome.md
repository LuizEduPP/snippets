---
tags: ["bash", "system", "chrome", "pwa", "gnome"]
---
# Remove Chrome PWA Desktop Apps

Detects and forces a complete wipe of isolated Progressive Web Apps (PWAs) integrated via Chrome interfaces, including GNOME-shell integrations.

## 🛠️ How it works under the hood

1. **PWA Integration**: When Chrome installs a webpage as a PWA, it doesn't just create a shortcut. It generates isolated `/opt` binary paths, caches local app data structures within `~/.config`, and routes desktop logic variables via local `.desktop` files.
2. **Explicit Deletion**: Regular uninstalls miss these sandboxed boundaries entirely. A clean wipe demands removing the core GNOME Chrome bridge and deleting the `.desktop` UI links from the standard XDG layout manually.

---

## 🚀 Usage Guide

### 1. Remove Chrome GNOME Core Packages
```bash
# Clean orphaned extensions on Debian/Ubuntu structures
sudo apt remove --purge chrome-gnome-shell -y
sudo apt autoremove -y

# Clean on Arch/Manjaro architectures
sudo pacman -Rns chrome-gnome-shell
```

### 2. Isolate Remaining Desktop Targets
Find exactly which UI links Google Chrome built for your environment.
```bash
ls ~/.local/share/applications/ | grep -i chrome
```

### 3. Annihilate Target PWA Variables
Remove every trace of the app (WhatsApp used as the target here).
```bash
# Delete the primary execution folder limits (if mapped globally)
sudo rm -rf /opt/WhatsAppWeb

# Wipe UI execution shortcuts
rm -f ~/.local/share/applications/WhatsAppWeb.desktop
sudo rm -f /usr/share/applications/WhatsAppWeb.desktop

# Nuke local caches, cookie variables, and sandboxed storage limits
rm -rf ~/.config/WhatsAppWeb ~/.cache/WhatsAppWeb ~/.local/share/WhatsAppWeb
```
