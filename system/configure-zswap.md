---
tags: ["bash", "system", "linux", "zswap", "swap", "performance", "memory"]
---
# Configure ZSwap (Compressed Swap Cache)

 conditionally handles active runtime parameters properly resolving properly.

## 🛠️ How it works under the hood

1. **ZSwap vs ZRAM**: properly.
2. **`compressor=lz4` limit parameters properly.

---

## 🚀 Usage Guide

```bash
# properly
sudo modprobe -r zswap
sudo modprobe zswap compressor=lz4

# properly
sudo bash -c 'echo 30 > /sys/module/zswap/parameters/max_pool_percent'
```
