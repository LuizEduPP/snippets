---
tags: ["bash", "system", "kde", "windows11", "theme", "kvantum"]
---
# KDE Windows 11 Style (Kvantum + WhiteSur)

Injects a complete Windows 11 visual overhaul over KDE Plasma's UI by linking Kvantum rendering pipelines to the WhiteSur GTK/Qt theme templates.

## 🛠️ How it works under the hood

1. **Theme Splitting**: Linux desktop environments mix Qt (KDE apps) and GTK (GNOME legacy apps). A uniform theme requires two configurations: `kvantum` forces SVG rendering for Qt apps, while `lxappearance` dictates variables for GTK clients.
2. **Kvantum Overrides**: Instead of relying on native Plasma decorators, Kvantum intercepts the memory draw cycles, applying custom blur, transparency, and flat borders matching the Win11 `.kvconfig` maps.

---

## 🚀 Usage Guide

### 1. Compile Display Engines
Install the necessary Kvantum rendering logic and WhiteSur packages (Arch/Manjaro).
```bash
# Core engines
sudo pacman -S kvantum-qt5 kvantum-qt6

# WhiteSur aesthetic templates
yay -S whitesur-kde-theme whitesur-gtk-theme whitesur-icon-theme
```

### 2. Configure the Qt Structure (Kvantum)
Load the Windows 11 logic into the engine.
```bash
# Prepare engine repositories
mkdir -p ~/.config/Kvantum/Win11OS-dark

# Route the downloaded `.kvconfig` into execution limits
mv ~/Downloads/Win11OS-dark.kvconfig ~/.config/Kvantum/Win11OS-dark/

# Execute Kvantum Manager to apply it graphically
kvantummanager
```

### 3. Normalize Legacy GTK Apps
Force cross-compatibility so GTK dialogs match the KDE theme.
```bash
# Select WhiteSur inside the GTK protocol manager
lxappearance
```

### 4. Global Fallback
Finish the sequence by setting the official global theme pointers.
```text
System Settings → Global Theme → WhiteSur
```
