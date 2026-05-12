---
tags: ["shell-linux", "system", "chrome", "pwa", "gnome"]
---
# Remove chrome-gnome-shell (Linux)

Removes the `chrome-gnome-shell` package and any related browser-integrated desktop apps installed as progressive web apps (PWAs), including those created from Chrome on Linux.

Paste and run directly in the terminal — no file needed.

## Command

### Remove the chrome-gnome-shell integration package

```bash
sudo apt remove --purge chrome-gnome-shell -y
sudo apt autoremove -y
```

---

### Remove a PWA installed via Chrome (e.g., WhatsApp Web)

```bash
# Remove the binary from /opt (if Chrome created one)
sudo rm -rf /opt/WhatsAppWeb

# Remove desktop shortcut (user)
rm -f ~/.local/share/applications/WhatsAppWeb.desktop

# Remove desktop shortcut (system-wide)
sudo rm -f /usr/share/applications/WhatsAppWeb.desktop

# Remove app data
rm -rf ~/.config/WhatsAppWeb ~/.cache/WhatsAppWeb ~/.local/share/WhatsAppWeb
```

---

## List all Chrome PWA shortcuts

```bash
ls ~/.local/share/applications/ | grep -i chrome
```

---

## Notes

- On Arch/Manjaro, use `sudo pacman -Rns chrome-gnome-shell` instead of `apt`.
- PWA names vary — look for `chrome-*.desktop` files in `~/.local/share/applications/`.
- After removal, refresh the desktop with `update-desktop-database ~/.local/share/applications/`.
