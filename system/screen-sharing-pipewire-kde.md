---
tags: ["bash", "system", "pipewire", "kde", "screen-sharing", "wayland"]
---
# Screen Sharing via PipeWire (KDE / Wayland)

Installs the required DBus portals required to buffer screen feeds inside Wayland, enabling desktop sharing for apps like Discord or OBS.

## 🛠️ How it works under the hood

1. **Wayland Privacy Protocol**: Unlike X11, Wayland is strictly compartmentalized. Apps cannot physically see your screen unless explicit portal logic is triggered.
2. **`xdg-desktop-portal`**: This acts as the secure interface. It exposes a generic DBus protocol that triggers the localized KDE screen picker dialogue, handing over exactly one screen buffer back to the requesting app via `pipewire` video pipelines.

---

## 🚀 Usage Guide

### 1. Configure Portal Dependencies
```bash
# Arch/Manjaro architectures
sudo pacman -S xdg-desktop-portal xdg-desktop-portal-kde pipewire wireplumber

# Debian/Ubuntu architectures
sudo apt install xdg-desktop-portal xdg-desktop-portal-kde pipewire wireplumber
```

### 2. Reboot the Portal Layer
Restart the local instance so the new portals lock into the live compositor.
```bash
systemctl --user restart xdg-desktop-portal
systemctl --user restart xdg-desktop-portal-kde
```

### 3. Force Legacy Apps into PipeWire
Many Electron apps (like Discord) default to legacy X11 capture buffers. Force them onto the new protocol. ```bash
# Launch Discord relying on Wayland
DISCORD_USE_PIPEWIRE=1 discord
```

### 4. Trace the Execution Graph
Verify that your specific KDE endpoints mapped. ```bash
systemctl --user status xdg-desktop-portal
systemctl --user status xdg-desktop-portal-kde
```
