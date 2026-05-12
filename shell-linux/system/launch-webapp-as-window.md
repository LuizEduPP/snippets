---
tags: ["shell-linux", "system", "chromium", "webapp", "desktop"]
---
# Launch Web App as Standalone Window (Chromium)

Opens a website as a standalone desktop window — no browser toolbar — using Chromium's `--app` flag. Works for WhatsApp Web, Gmail, Notion, and any other web app.

Paste and run directly in the terminal — no file needed.

## Command

```bash
chromium --app=https://web.whatsapp.com
```

```bash
# Also works with Google Chrome
google-chrome --app=https://web.whatsapp.com
```

---

## Create a desktop shortcut

```bash
cat > ~/.local/share/applications/whatsapp-web.desktop << 'EOF'
[Desktop Entry]
Name=WhatsApp Web
Exec=chromium --app=https://web.whatsapp.com
Icon=chromium
Terminal=false
Type=Application
Categories=Network;
EOF

# Refresh desktop database
update-desktop-database ~/.local/share/applications/
```

### Generic template (change URL and Name)

```bash
APP_NAME="Gmail"
APP_URL="https://mail.google.com"
SLUG="gmail"

cat > ~/.local/share/applications/${SLUG}.desktop << EOF
[Desktop Entry]
Name=${APP_NAME}
Exec=chromium --app=${APP_URL}
Icon=chromium
Terminal=false
Type=Application
Categories=Network;
EOF

update-desktop-database ~/.local/share/applications/
```

---

## Notes

- The window has no address bar, tabs, or browser UI — behaves like a native app.
- The shortcut appears in your app launcher after `update-desktop-database`.
- Replace `chromium` with `google-chrome`, `brave`, or `chromium-browser` depending on your installation.
