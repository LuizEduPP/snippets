---
tags: ["bash", "system", "kde", "ubuntu", "install"]
---
# Install KDE Plasma on Ubuntu / Zorin OS

Deploys the KDE Plasma environment replacing or coexisting alongside default GNOME window managers. ## 🛠️ How it works under the hood

1. **Display Managers (SDDM vs GDM)**: Upon boot, graphical logic is caught by a login screen (Display Manager). Plasma typically ships with SDDM creating a distinct session endpoint before routing strictly into KWin / Qt5 composition boundaries safely replacing GNOME's Mutter.

---

## 🚀 Usage Guide

### Install Desktop Environments
```bash
# Update primary packages safely
sudo apt update

# Option 1: Standard clean Plasma desktop
sudo apt install kde-plasma-desktop

# Option 2: Core structure minimal packages
sudo apt install kde-plasma-desktop --no-install-recommends

# Option 3: Full KDE Software suite
sudo apt install kde-full
```

### Clean up and Revert Actions
```bash
# If transitioning back to GNOME is required, clean orphaned Qt logic safely
sudo apt remove --purge kde-plasma-desktop kde-full

sudo apt autoremove
```
