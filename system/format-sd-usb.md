---
tags: ["bash", "system", "format", "usb", "sd-card"]
---
# Format SD Card or USB Drive (Linux)

Instantly formats external storage devices as FAT32, exFAT, or ext4 directly through the Linux terminal, ensuring clean partition tables.

## 🛠️ How it works under the hood

1. **`mkfs` (Make File System)**: The raw kernel utility writes a fresh filesystem layout over the chosen block device tracking layer.
2. **Block isolation**: A storage drive must be forcibly unmounted (`umount`) so the kernel releases its I/O lock, allowing the formatting process to overwrite the block headers safely.

---

## 🚀 Usage Guide

### 1. Identify and Unmount
```bash
# Find your target device (e.g., /dev/sdb1)
lsblk

# Release the kernel lock
sudo umount /dev/sdX1
```

### 2. Format the Device
```bash
# FAT32 (Best for smaller USBs <= 32GB, maximum compatibility)
sudo mkfs.vfat -F 32 /dev/sdX1

# exFAT (Best for large drives > 32GB, Windows/Mac support)
sudo mkfs.exfat /dev/sdX1

# ext4 (Linux only, supports file permissions)
sudo mkfs.ext4 /dev/sdX1
```

### 3. Wipe corrupted tables
If the drive fails to format, clean its raw partition table first.
```bash
sudo wipefs -a /dev/sdX
```
