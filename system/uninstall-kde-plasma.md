---
tags: ["bash", "system", "kde", "uninstall"]
---
# Uninstall KDE Plasma (Ubuntu / Debian)

Completely removes the KDE Plasma desktop framework blocks and localized QT packages, falling back to the baseline generic DE installation limits. ## 🛠️ How it works under the hood

1. **Mass Package Purging Options**: Similar to simple binary cleanup limits, executing absolute removal definitions over large meta-packages (`plasma-workspace`) fundamentally unmaps the display UI boundaries directly. APT cascades logic resolving explicit dependency chains locally.

---

## 🚀 Usage Guide

### 1. View Assigned Boundaries
Confirm local structures mapped directly to the active system cache.
```bash
dpkg -l | grep kde
dpkg -l | grep plasma
```

### 2. Lock Massive System Definitions Out
Target the absolute meta-package core native variables out of the local cache inherently.
```bash
sudo apt remove --purge -y \
 kde-plasma-desktop plasma-desktop plasma-workspace \
 plasma-discover plasma-systemmonitor plasma-pa plasma-integration \
 plasma-thunderbolt plasma-disks plasma-browser-integration \
 kde-baseapps kde-cli-tools kde-config-gtk-style kde-config-screenlocker \
 kde-config-sddm kde-config-updates polkit-kde-agent-1 \
 kde-style-breeze kde-style-oxygen-qt5 kdeconnect \
 xdg-desktop-portal-kde kded5 libkf5plasma5 libkf5plasmaquick5 \
 plasma-framework libplasma-geolocation-interface5

# Clean cascading local node values sudo apt autoremove --purge -y
```

### 3. Diagnose Structural Errors
In case dependency cycles get fundamentally broken during absolute cascades, rebuild native caches inherently.
```bash
sudo apt update
sudo apt --fix-broken install
sudo dpkg --configure -a
sudo apt autoremove --purge -y
sudo apt clean
```

### 4. Restart Execution Limits
Lock changes in and restart locally to trigger base login boundaries completely.
```bash
sudo apt full-upgrade -y
sudo reboot
```
> Select GNOME (or your pure base DE limits) via the display manager login cog icon locally.
