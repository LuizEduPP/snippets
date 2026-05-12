---
tags: ["shell-linux", "system", "zram", "ram", "performance"]
---
# Optimize RAM — ZRAM + Swappiness (Linux)

Enables ZRAM (compressed in-RAM swap) and tunes the swappiness kernel parameter to improve performance on systems with limited RAM or heavy IDE usage.

Paste and run directly in the terminal — no file needed.

## Command

### Enable ZRAM (systemd-based — Arch/Manjaro/Ubuntu 22.04+)

```bash
sudo systemctl enable --now systemd-zram-setup@zram0
```

### Manual ZRAM setup (older systems)

```bash
# Load the zram module on boot
echo 'zram' | sudo tee /etc/modules-load.d/zram.conf
echo 'options zram num_devices=1' | sudo tee /etc/modprobe.d/zram.conf
```

---

### Reduce swappiness (default is 60; lower = prefer RAM)

```bash
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

> `swappiness=10` means the kernel only uses swap when RAM is 90%+ full.

---

### Drop page cache (free memory without rebooting)

```bash
sudo sync && echo 3 | sudo tee /proc/sys/vm/drop_caches
```

---

### Monitor memory

```bash
free -h                              # summary
htop                                 # interactive
ps aux --sort=-%mem | head -20       # top memory consumers
```

---

## VS Code / IDE memory limits

Add to VS Code `settings.json` to cap extension host memory:

```json
{
    "editor.maxMemory": 2048,
    "typescript.tsserver.maxTsServerMemory": 2048,
    "search.maxResults": 100
}
```
