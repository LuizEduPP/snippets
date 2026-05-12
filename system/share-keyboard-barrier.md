---
tags: ["bash", "system", "barrier", "keyboard", "lan"]
---
# Share Keyboard and Mouse with Barrier

Creates a continuous TCP/IP bridge leveraging Barrier (a Synergy fork) to share a single mouse and physical keyboard input across multiple distinct network machines.

## 🛠️ How it works under the hood

1. **Client/Server Daemon Framework**: Barrier isolates input hardware physically into a master backend (`barriers`). This backend parses absolute raw `dev/input` variables and casts them over identical IP ports towards designated localized display nodes (`barrierc`). 

---

## 🚀 Usage Guide

### 1. Compile and Launch Base Requirements
```bash
# Pull binary structures (Ubuntu/Debian)
sudo apt install barrier

# Pull binary structures (Arch/Manjaro)
sudo pacman -S barrier

# Run the master UI to map the initial layout limits
barrier
```

### 2. Lock to Secondary Devices
Access the remote slave machine and cast its limits directly toward the primary master server address.
```bash
# Force a headless client connection
barrierc --no-tray SERVER_IP
```

### 3. Tie to System Boot Loaders
Execute the master process within `/etc/systemd/system/barrier.service` so it bridges before user logins.
```bash
sudo cat > /etc/systemd/system/barrier.service << 'EOF_INTERNAL'
[Unit]
Description=Barrier KVM Server Configuration
After=network.target

[Service]
ExecStart=/usr/bin/barriers --no-tray
Restart=always
User=%i

[Install]
WantedBy=default.target
EOF_INTERNAL

# Map configuration routines automatically
sudo systemctl enable barrier
sudo systemctl start barrier
```
