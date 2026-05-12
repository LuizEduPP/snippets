---
tags: ["shell-linux", "system", "xdg", "file-manager", "dolphin"]
---
# Set Default File Manager (Linux)

Changes the default file manager application used when opening folders from the desktop, terminal, or other apps.

Paste and run directly in the terminal — no file needed.

## Command

### Install Dolphin (if not installed)

```bash
# Debian/Ubuntu/Zorin
sudo apt install dolphin

# Arch/Manjaro
sudo pacman -S dolphin
```

### Set Dolphin as the default file manager

```bash
xdg-mime default dolphin.desktop inode/directory
xdg-mime default dolphin.desktop application/x-directory
```

### Set Nautilus (GNOME Files)

```bash
xdg-mime default nautilus.desktop inode/directory
```

### Set Thunar (Xfce)

```bash
xdg-mime default thunar.desktop inode/directory
```

### Set Nemo (Cinnamon)

```bash
xdg-mime default nemo.desktop inode/directory
```

---

### Verify the current default

```bash
xdg-mime query default inode/directory
```

---

### System-wide (KDE Plasma settings)

```
System Settings → Applications → Default Applications → File Manager
```

---

## Notes

- The `.desktop` filename must match what's installed in `/usr/share/applications/` — verify with `ls /usr/share/applications/ | grep -i dolphin`.
- On GNOME/Zorin, you can also use **Settings → Default Applications**.
- Changes take effect immediately for new file open actions.
