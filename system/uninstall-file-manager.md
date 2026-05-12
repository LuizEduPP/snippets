---
tags: ["bash", "system", "dolphin", "uninstall", "packages"]
---
# Uninstall Dolphin or Nemo File Manager

Completely strips secondary file managers (Dolphin for KDE or Nemo for Cinnamon) including orphaned dependencies and isolated caching nodes in Linux.

## 🛠️ How it works under the hood

1. **APT Package Removal Arrays**: Standard `.deb` packaging isolates binaries and core structural libraries. The `--purge` command inherently forces standard local nodes mapping configuration files generated within `/etc` to detach, wiping trace files entirely. Local user space configuration blocks (like `~/.config`) must be forcibly executed out directly because Debian packaging ignores user boundaries intentionally.

---

## 🚀 Usage Guide

### 1. Execute Uninstall Boundaries (Dolphin / KDE)
Remove binary arrays tied to Plasma.
```bash
sudo apt remove --purge \
 dolphin \
 dolphin-plugins \
 kde-cli-tools \
 kde-runtime \
 kio* \
 konsole*
```

Force pure user space node cleanup.
```bash
rm -rf ~/.config/dolphin
rm -rf ~/.local/share/dolphin
rm -rf ~/.kde
rm -rf ~/.kde4
```

### 2. Execute Uninstall Boundaries (Nemo / Cinnamon)
Remove binary arrays tied to GTK layers.
```bash
sudo apt remove --purge \
 nemo \
 nemo-* \
 cinnamon-desktop-data \
 cinnamon-translations
```

Force pure user space node cleanup.
```bash
rm -rf ~/.config/nemo
rm -rf ~/.local/share/nemo
rm -rf ~/.cinnamon
```

### 3. Diagnose Broken Orphans
Standard dependency boundaries sometimes persist. Clear them using absolute tools. ```bash
# Clear normal cache structures
sudo apt autoremove --purge
sudo apt clean && sudo apt update

# Target detached orphans sudo apt install deborphan
sudo apt remove --purge $(deborphan)
```
