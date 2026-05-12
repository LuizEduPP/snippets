---
tags: ["bash", "system", "ram", "memtester", "hardware"]
---
# Test RAM with memtester

Executes explicit stress boundaries locally on Linux physical RAM sectors, isolating hardware corruption without requiring persistent offline generic boot limits.

## 🛠️ How it works under the hood

1. **`memtester` validation arrays**: Instead of allocating OS memory sequentially, it claims absolute predefined block targets and executes continuous read/write comparison loops physically hammering specific voltages. If absolute values mismatch when actively resolving bit tests, it identifies decaying memory node arrays.

---

## 🚀 Usage Guide

### 1. Execute Dependency
```bash
# Ubuntu/Debian
sudo apt install memtester

# Arch/Manjaro
sudo pacman -S memtester
```

### 2. Lock and Stream Memory Load testing
Pass explicit limits inside the terminal.
```bash
# Force 1 Gigabyte of testing across 4 explicit load tests
sudo memtester 1G 4

# Scale absolute maximums up to extreme thresholds
sudo memtester 2G 4 # 2 GB, 4 passes
sudo memtester 4G 10 # 4 GB, 10 passes (thorough)
```

### 3. Diagnose Feedback Arrays
Watch for the active output mapping local test routines.
```text
Loop 1/4: ok
Loop 2/4: ok
Loop 3/4: ok
Done.
```
> If any loop states `FAILURE`, memory is inherently decaying physically. Testing individual sticks isolating the hardware is heavily required.
