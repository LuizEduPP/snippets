---
tags: ["shell-linux", "system", "kde", "theme", "kvantum"]
---
# Install Fluent KDE Theme (Manjaro)

Installs the Fluent theme for KDE Plasma using Kvantum for Qt apps and the official Fluent icon set.

Paste and run directly in the terminal — no file needed.

## Command

### Install dependencies

```bash
sudo pacman -S --needed git kvantum-qt6 qt6ct fluent-icon-theme
```

### Clone and install the Fluent KDE theme

```bash
git clone https://github.com/vinceliuice/Fluent-kde.git ~/Downloads/Fluent-kde
cd ~/Downloads/Fluent-kde

# Install dark variant with Kvantum support
./install.sh --dark --kvantum
```

### Apply the Kvantum theme

```bash
kvantummanager
```

> In Kvantum Manager: **Change/Delete Theme** → select `Fluent-dark` → **Use this theme**.

### Apply via `~/.config/kdeglobals`

```ini
[Appearance]
style=kvantum
icon_theme=Fluent-dark
```

---

## Variants

```bash
./install.sh           # light
./install.sh --dark    # dark
./install.sh --round   # rounded corners
./install.sh --dark --round  # dark + rounded
```
