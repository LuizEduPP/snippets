---
tags: ["shell-linux", "system", "ssh", "rdp", "remote"]
---
# Remote Access over LAN (SSH + RDP)

Connects two computers on the same local network using SSH (terminal) or RDP (full desktop).

Paste and run directly in the terminal — no file needed.

---

## SSH — Terminal access

### Linux server setup

```bash
sudo apt install openssh-server   # Debian/Ubuntu
sudo pacman -S openssh            # Arch/Manjaro

sudo systemctl enable --now ssh

# Find the server IP
ip addr
```

### Connect from any OS

```bash
# From Linux or macOS terminal
ssh user@192.168.0.100

# From Windows (PowerShell or CMD)
ssh user@192.168.0.100
```

---

## RDP — Full desktop access

### Access a Windows machine from Linux

```bash
# Arch/Manjaro
sudo pacman -S remmina freerdp

# Debian/Ubuntu
sudo apt install remmina freerdp2-x11

# Connect via command line
xfreerdp /v:192.168.0.105 /u:USERNAME /p:PASSWORD

# Or open Remmina GUI
remmina
```

### Access a Linux machine from Windows

Install xrdp on the Linux machine:

```bash
sudo apt install xrdp              # Debian/Ubuntu
sudo pacman -S xrdp                # Arch/Manjaro (AUR)

sudo systemctl enable --now xrdp
```

Then on Windows, open **Remote Desktop Connection** (`mstsc`) and enter the Linux machine's IP.

---

## Find local IP addresses

```bash
# Linux
ip addr
hostname -I

# Windows (cmd)
ipconfig
```
