---
tags: ["shell-linux", "system", "ram", "memtester", "hardware"]
---
# Test RAM with memtester

Runs a memory stress test on Linux to detect faulty RAM modules without rebooting into a live environment.

Paste and run directly in the terminal — no file needed.

## Install

```bash
# Debian/Ubuntu/Zorin
sudo apt install memtester

# Arch/Manjaro
sudo pacman -S memtester
```

## Command

### Test 1 GB of RAM, 4 passes

```bash
sudo memtester 1G 4
```

### Test more memory or more passes

```bash
sudo memtester 2G 4    # 2 GB, 4 passes
sudo memtester 4G 10   # 4 GB, 10 passes (thorough)
```

> The larger the amount and more passes, the longer the test. Rule of thumb: test at least 75% of total RAM.

### Expected healthy output

```
Loop 1/4: ok
Loop 2/4: ok
Loop 3/4: ok
Loop 4/4: ok
Done.
```

A `FAILURE` line on any test indicates faulty RAM at that address.

---

## Monitor memory usage while testing

```bash
# In a separate terminal
free -h
htop
```

---

## Notes

- You cannot test memory that is currently in use by the OS. For a full test, use **Memtest86+** from a bootable USB.
- If `memtester` reports failures, try one stick at a time to isolate the bad module.
