---
tags: ["shell-linux", "system", "kde", "kwin", "theme"]
---
# Fix KDE Window Borders / Decorations

Restores missing window borders and title bars in KDE Plasma after a theme change, KWin crash, or misconfigured setting.

Paste and run directly in the terminal — no file needed.

## Command

### Restore maximized window borders

```bash
kwriteconfig5 --file kwinrc --group Windows --key BorderlessMaximizedWindows false
qdbus org.kde.KWin /KWin reconfigure
```

### Restart KWin (X11)

```bash
kwin_x11 --replace &
```

### Restart KWin (Wayland)

```bash
kwin_wayland --replace &
```

---

### Reset KWin config (last resort)

```bash
mv ~/.config/kwinrc ~/.config/kwinrc.bkp
qdbus org.kde.KWin /KWin reconfigure
```

### Restart Plasma shell

```bash
plasmashell --replace & disown
```

---

## Notes

- If the issue appeared after switching to a Kvantum or GTK theme, check **System Settings → Window Decorations** and re-select a KWin decoration (e.g., Breeze).
- On Wayland, `qdbus` may not be available — use `kwin_wayland --replace &` directly.
- Backspace the `.bkp` rename if the reset doesn't help: `mv ~/.config/kwinrc.bkp ~/.config/kwinrc`.
