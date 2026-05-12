---
tags: ["shell-linux", "system", "barrier", "keyboard", "lan"]
---
# Share Keyboard and Mouse with Barrier

Runs [Barrier](https://github.com/debauchee/barrier) as a persistent systemd service so one keyboard and mouse control multiple computers on the same network.

Paste and run directly in the terminal — no file needed.

## Command

### Install

```bash
# Debian/Ubuntu
sudo apt install barrier

# Arch/Manjaro
sudo pacman -S barrier
```

### Run the GUI to configure (server side)

```bash
barrier
```

Set the server to listen and place the client screens in the layout. Note the server IP address.

### Connect from the client machine

```bash
barrierc --no-tray SERVER_IP
```

---

## Run as a systemd service (auto-start on login)

```bash
sudo nano /etc/systemd/system/barrier.service
```

Paste:

```ini
[Unit]
Description=Barrier KVM Server
After=network.target

[Service]
ExecStart=/usr/bin/barriers --no-tray
Restart=always
User=%i

[Install]
WantedBy=default.target
```

Enable and start:

```bash
sudo systemctl enable barrier
sudo systemctl start barrier
```
