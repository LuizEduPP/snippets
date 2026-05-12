---
tags: ["shell-linux", "system", "kde", "windows11", "theme", "kvantum"]
---
# KDE Windows 11 Style (Kvantum + WhiteSur)

Applies a Windows 11-inspired visual style to KDE Plasma using Kvantum themes and the WhiteSur GTK/KDE theme pack.

Paste and run directly in the terminal — no file needed.

## Command

### Install Kvantum (Arch/Manjaro)

```bash
sudo pacman -S kvantum-qt5 kvantum-qt6
```

### Install WhiteSur KDE + GTK theme (AUR)

```bash
yay -S whitesur-kde-theme whitesur-gtk-theme whitesur-icon-theme
```

---

### Apply a custom Kvantum theme (manual install)

```bash
# Create Kvantum config directory
mkdir -p ~/.config/Kvantum

# Copy downloaded theme
mkdir -p ~/.config/Kvantum/Win11OS-dark
mv ~/Downloads/Win11OS-dark.kvconfig ~/.config/Kvantum/Win11OS-dark/

# Open Kvantum Manager and select the theme
kvantummanager
```

> In Kvantum Manager: **Change/Delete Theme** → select `Win11OS-dark` → **Use this theme**.

---

### Apply GTK theme with lxappearance

```bash
lxappearance
```

> Select WhiteSur as the GTK theme for apps like Nautilus, Thunar, and GTK-based dialogs.

---

### Apply the KDE Global Theme

```
System Settings → Global Theme → WhiteSur
```

---

## Notes

- Kvantum handles Qt5/Qt6 apps (e.g., Dolphin, Kate, Okular). GTK theme handles GTK apps.
- For the Windows 11 taskbar style, also install the **Latte Dock** or use the default KDE panel with **Windows 11 plasmoid**.
- `yay` can be replaced with `pamac install` on Manjaro.
