---
tags: ["shell-linux", "system", "kde", "themes"]
---
# Check Active GTK and Qt Themes

Reads the user's theme configuration files and prints the active theme for **GTK 2**, **GTK 3**, **GTK 4**, **Qt5**, and **Qt6**.

Paste and run directly in the terminal — no file needed.

## Expected output

```
Checking GTK and Qt themes...
--------------------------------------------

GTK 2:
gtk-theme-name="Adwaita-dark"
gtk-icon-theme-name="Papirus-Dark"

GTK 3:
gtk-theme-name=Adwaita-dark
icon-theme-name=Papirus-Dark
cursor-theme-name=Bibata-Modern-Classic

GTK 4:
gtk-theme-name=Adwaita-dark

Qt5 (qt5ct):
style=Fusion
icon_theme=Papirus-Dark

Qt6 (qt6ct):
style=Fusion
icon_theme=Papirus-Dark
```

## Config files read

| Toolkit | File |
|---------|------|
| GTK 2 | `~/.gtkrc-2.0` |
| GTK 3 | `~/.config/gtk-3.0/settings.ini` |
| GTK 4 | `~/.config/gtk-4.0/settings.ini` |
| Qt5 | `~/.config/qt5ct/qt5ct.conf` |
| Qt6 | `~/.config/qt6ct/qt6ct.conf` |

## Command

```bash
echo "Checking GTK and Qt themes..."
echo "--------------------------------------------"

echo -e "\nGTK 2:"
gtkrc="$HOME/.gtkrc-2.0"
[ -f "$gtkrc" ] && grep -E 'gtk-theme-name|gtk-icon-theme-name|gtk-font-name' "$gtkrc" || echo "File not found: $gtkrc"

echo -e "\nGTK 3:"
gtk3="$HOME/.config/gtk-3.0/settings.ini"
[ -f "$gtk3" ] && grep -E 'gtk-theme-name|icon-theme-name|cursor-theme-name' "$gtk3" || echo "File not found: $gtk3"

echo -e "\nGTK 4:"
gtk4="$HOME/.config/gtk-4.0/settings.ini"
[ -f "$gtk4" ] && grep -E 'gtk-theme-name|icon-theme-name|cursor-theme-name' "$gtk4" || echo "File not found: $gtk4"

echo -e "\nQt5 (qt5ct):"
qt5ct="$HOME/.config/qt5ct/qt5ct.conf"
[ -f "$qt5ct" ] && grep -E 'style|icon_theme' "$qt5ct" || echo "File not found: $qt5ct"

echo -e "\nQt6 (qt6ct):"
qt6ct="$HOME/.config/qt6ct/qt6ct.conf"
[ -f "$qt6ct" ] && grep -E 'style|icon_theme' "$qt6ct" || echo "File not found: $qt6ct"
```
