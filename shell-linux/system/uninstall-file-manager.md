---
tags: ["shell-linux", "system", "dolphin", "uninstall", "packages"]
---
# Uninstall Dolphin or Nemo File Manager

Completely removes Dolphin (KDE) or Nemo (Cinnamon) including their dependencies and configuration directories.

Paste and run directly in the terminal — no file needed.

## Command

### Remove Dolphin (KDE)

```bash
sudo apt remove --purge \
    dolphin \
    dolphin-plugins \
    kde-cli-tools \
    kde-runtime \
    kio* \
    konsole*
```

Clean up leftover KDE config:

```bash
rm -rf ~/.config/dolphin
rm -rf ~/.local/share/dolphin
rm -rf ~/.kde
rm -rf ~/.kde4
```

### Remove Nemo (Cinnamon)

```bash
sudo apt remove --purge \
    nemo \
    nemo-* \
    cinnamon-desktop-data \
    cinnamon-translations
```

Clean up leftover Nemo config:

```bash
rm -rf ~/.config/nemo
rm -rf ~/.local/share/nemo
rm -rf ~/.cinnamon
```

---

## Clean up after removal

```bash
# Remove unused dependencies
sudo apt autoremove --purge

# Clear package cache
sudo apt clean && sudo apt update
```

### Find and remove orphan packages (deborphan)

```bash
sudo apt install deborphan

# List orphans
deborphan

# Remove all orphans
sudo apt remove --purge $(deborphan)
```

### Verify no leftover packages remain

```bash
# Check for Dolphin/KDE leftovers
dpkg -l | grep -E "dolphin|kde|kio"

# Check for Nemo/Cinnamon leftovers
dpkg -l | grep -E "nemo|cinnamon"
```
