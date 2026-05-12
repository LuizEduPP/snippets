---
tags: ["shell-linux", "system", "zswap", "swap", "performance"]
---
# Configure ZSwap (Compressed Swap Cache)

Enables and tunes ZSwap — a Linux kernel feature that compresses swap pages in RAM before writing them to disk, improving performance compared to raw swap.

Paste and run directly in the terminal — no file needed.

## Command

### Check current ZSwap status

```bash
cat /sys/module/zswap/parameters/enabled
cat /sys/module/zswap/parameters/compressor
cat /sys/module/zswap/parameters/max_pool_percent
```

### Change compressor at runtime

```bash
sudo modprobe -r zswap
sudo modprobe zswap compressor=lz4
```

Available compressors: `lz4` (fastest), `zstd` (best ratio), `lzo` (default).

### Increase memory pool size at runtime

```bash
sudo bash -c 'echo 30 > /sys/module/zswap/parameters/max_pool_percent'
```

---

### Make settings persistent via GRUB

Edit `/etc/default/grub`:

```bash
sudo nano /etc/default/grub
```

Add to `GRUB_CMDLINE_LINUX_DEFAULT`:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet zswap.enabled=1 zswap.compressor=lz4 zswap.max_pool_percent=30"
```

Apply:

```bash
sudo update-grub
```

---

## Notes

- ZSwap is different from ZRAM: ZSwap compresses pages before they go to disk swap; ZRAM replaces swap entirely with a compressed RAM device.
- `lz4` is recommended for speed; use `zstd` for better compression on memory-constrained systems.
- Default pool is 20% of RAM. 25–30% is a safe increase for most desktops.
