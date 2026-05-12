---
tags: ["shell-linux", "system", "pipewire", "kde", "screen-sharing", "wayland"]
---
# Screen Sharing via PipeWire (KDE / Wayland)

Enables screen sharing in apps like Discord, Google Meet, and OBS on KDE Plasma with Wayland by installing the required PipeWire portals.

Paste and run directly in the terminal — no file needed.

## Command

### Install PipeWire screen capture stack (Arch/Manjaro)

```bash
sudo pacman -S xdg-desktop-portal xdg-desktop-portal-kde pipewire wireplumber
```

### Debian/Ubuntu

```bash
sudo apt install xdg-desktop-portal xdg-desktop-portal-kde pipewire wireplumber
```

### Restart the portal service

```bash
systemctl --user restart xdg-desktop-portal
systemctl --user restart xdg-desktop-portal-kde
```

---

## Launch Discord with PipeWire support

```bash
DISCORD_USE_PIPEWIRE=1 discord
```

> Or add `DISCORD_USE_PIPEWIRE=1` to your system environment (`/etc/environment`) to make it permanent.

---

## Troubleshoot — check if portals are running

```bash
systemctl --user status xdg-desktop-portal
systemctl --user status xdg-desktop-portal-kde
```

---

## Notes

- `xdg-desktop-portal-kde` handles the screen picker dialog on KDE Wayland. For GNOME, use `xdg-desktop-portal-gnome` instead.
- If you have multiple portals installed (e.g., `-kde` and `-gtk`), only one should be active at a time — see `/usr/lib/systemd/user/xdg-desktop-portal.service`.
- Reboot after installation if the portal service still refuses to share the screen.
