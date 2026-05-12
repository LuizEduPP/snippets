---
tags: ["shell-linux", "system", "kde", "uninstall"]
---
# Uninstall KDE Plasma (Ubuntu / Zorin)

Completely removes the KDE Plasma desktop environment and its packages from an Ubuntu-based system, leaving only the base DE (e.g., GNOME/XFCE).

Paste and run directly in the terminal — no file needed.

## Command

### List installed KDE/Plasma packages first

```bash
dpkg -l | grep kde
dpkg -l | grep plasma
```

### Remove KDE Plasma and related packages

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

sudo apt autoremove --purge -y
```

### Fix any broken packages

```bash
sudo apt update
sudo apt --fix-broken install
sudo dpkg --configure -a
sudo apt autoremove --purge -y
sudo apt clean
```

### Upgrade and reboot

```bash
sudo apt full-upgrade -y
sudo reboot
```

> After reboot, select your original desktop environment (GNOME, XFCE, etc.) on the login screen.
