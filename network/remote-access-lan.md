---
tags: ["bash", "network", "ssh", "rdp", "remote"]
---
# Remote Access over LAN (SSH + RDP)

Establishes terminal-based endpoints through SSH or remote display interactions via RDP protocols crossing isolated networking domains.

## 🛠️ How it works under the hood

1. **SSH daemon**: The OpenSSH background service listens internally over port 22, managing cryptographic key negotiation paths ensuring remote bash connections exchange data. 2. **xrdp services**: Wraps host Linux display modules (like X11/Wayland) with standard Microsoft RDP translation bindings executing virtual remote desktop instances on identical Windows client structures.

---

## 🚀 Usage Guide

### 1. Establish SSH Tunnels
Run inside target host servers. ```bash
# Apply packages internally on Debian/Ubuntu
sudo apt install openssh-server

# Apply packages internally on Arch/Manjaro
sudo pacman -S openssh

# Initialize background listeners inherently
sudo systemctl enable --now ssh
```

Connect remotely using standard client calls.
```bash
# Connect parsing specific IP limits
ssh user@192.168.0.100
```

### 2. Configure RDP (Linux accessing Windows)
Install the host display engine parser binaries. ```bash
# Setup Arch UI bounds
sudo pacman -S remmina freerdp

# Setup Ubuntu UI bounds
sudo apt install remmina freerdp2-x11

# Launch virtual instances targeting raw parameters xfreerdp /v:192.168.0.105 /u:USERNAME /p:PASSWORD
```

### 3. Configure XRDP (Windows accessing Linux)
Force the Linux kernel to expose Microsoft limits over port 3389.
```bash
# Initialize daemon handlers sudo apt install xrdp
sudo systemctl enable --now xrdp
```
Connect via Windows utilizing standard GUI tool logic (`mstsc`).
