---
tags: ["shell-linux", "system", "appimage", "desktop"]
---
# Create Desktop Shortcut for AppImage

Creates a `.desktop` entry so an AppImage appears in the application menu of any Linux desktop environment.

Paste and run directly in the terminal — no file needed.

## Command

### Make the AppImage executable

```bash
chmod +x /path/to/app.AppImage
```

### Create the .desktop file

Replace the values in `<...>` with your app details.

```bash
cat > ~/.local/share/applications/myapp.desktop << 'EOF'
[Desktop Entry]
Name=<App Name>
Comment=<Short description>
Exec=/path/to/app.AppImage
Icon=<icon-name-or-path>
Terminal=false
Type=Application
Categories=Utility;
StartupNotify=true
EOF
```

### Refresh the application menu

```bash
update-desktop-database ~/.local/share/applications
```

---

## Example — Cursor IDE

```bash
chmod +x ~/Cursor-0.49.6-x86_64.AppImage

cat > ~/.local/share/applications/cursor.desktop << 'EOF'
[Desktop Entry]
Name=Cursor IDE
Comment=AI-Powered Code Editor
Exec=/home/YOUR_USER/Cursor-0.49.6-x86_64.AppImage
Icon=cursor
Terminal=false
Type=Application
Categories=Development;IDE;Programming;
StartupNotify=true
EOF

update-desktop-database ~/.local/share/applications
```

> For the `Icon` field you can use a full path to a `.png` file instead of an icon name: `Icon=/path/to/icon.png`
