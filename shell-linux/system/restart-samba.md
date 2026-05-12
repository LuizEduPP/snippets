---
tags: ["shell-linux", "system", "samba", "network", "smb"]
---
# Restart Samba (Linux)

Restarts the Samba file-sharing service and verifies it is running correctly.

Paste and run directly in the terminal — no file needed.

## Command

### Restart

```bash
sudo systemctl restart smbd nmbd
```

### Check status

```bash
sudo systemctl status smbd
```

### Test configuration file

```bash
testparm
```

### List active shares

```bash
smbclient -L localhost
```

---

### Enable Samba to start on boot

```bash
sudo systemctl enable smbd nmbd
```
