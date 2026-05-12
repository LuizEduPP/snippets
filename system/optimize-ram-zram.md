---
tags: ["bash", "system", "zram", "ram", "performance"]
---
# Optimize RAM — ZRAM + Swappiness (Linux)

Allocates compressed synthetic RAM blocks (ZRAM) and configures Linux kernel swappiness logic to prevent system hangs on machines with low memory.

## 🛠️ How it works under the hood

1. **ZRAM**: Instead of writing overflow memory to a slow physical disk (standard swap), ZRAM creates a virtual block device directly in RAM. It aggressively compresses data pages on the fly, multiplying available memory capacity at the cost of slight CPU overhead.
2. **`vm.swappiness`**: This kernel parameter dictates how quickly the OS writes cache pages to swap. The default (`60`) writes early. Lowering it forces the kernel to exhaust physical RAM limits before caching data out, speeding up standard graphical computing load.

---

## 🚀 Usage Guide

### 1. Enable System-Level Block Compression
On systemd-based distros (Arch, Manjaro, Ubuntu 22.04+).
```bash
sudo systemctl enable --now systemd-zram-setup@zram0
```

### 2. Configure Aggressive Swappiness Values
Push the execution limits to rely entirely on rapid physical RAM limits.
```bash
# Append limits to the sysctl boundary file
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf

# Reload the kernel boundaries immediately
sudo sysctl -p
```
> `swappiness=10` instructs the kernel to only offload data when RAM reaches ~90% capacity.

### 3. Clear Stagnant Cache Manually
Flush lingering cache memory blocks without rebooting.
```bash
sudo sync && echo 3 | sudo tee /proc/sys/vm/drop_caches
```

### 4. Monitor Architecture Workload
```bash
# View human-readable capacity output
free -h

# Check top memory consumers by percentage
ps aux --sort=-%mem | head -20
```
