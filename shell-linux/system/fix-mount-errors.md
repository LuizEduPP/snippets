---
tags: ["shell-linux", "system", "mount", "ntfs", "fsck"]
---
# Fix Partition Mount Errors

Diagnoses and repairs common mount failures for NTFS, exFAT, ext4, and Btrfs partitions.

Paste and run directly in the terminal — no file needed.

## Diagnose first

```bash
# Check the filesystem type
sudo blkid /dev/sdX1

# Check kernel messages for mount errors
sudo dmesg | tail -30 | grep -i sdX1

# Check system logs
sudo journalctl -xe | grep mount
```

---

## NTFS

```bash
# Install driver (Arch/Manjaro)
sudo pacman -S ntfs-3g

# Install driver (Debian/Ubuntu)
sudo apt install ntfs-3g

# Repair
sudo ntfsfix /dev/sdX1

# Mount
sudo mount -t ntfs-3g /dev/sdX1 /mnt
```

## exFAT

```bash
# Install tools (Arch/Manjaro)
sudo pacman -S exfatprogs

# Install tools (Debian/Ubuntu)
sudo apt install exfat-fuse exfatprogs

# Repair
sudo fsck.exfat /dev/sdX1

# Mount
sudo mount -t exfat /dev/sdX1 /mnt
```

## ext4

```bash
# Repair
sudo e2fsck -f /dev/sdX1

# If superblock is corrupted, use backup superblock
sudo dumpe2fs /dev/sdX1 | grep superblock
sudo e2fsck -b 32768 /dev/sdX1

# Mount
sudo mount -t ext4 /dev/sdX1 /mnt
```

## Btrfs

```bash
# Install tools (Arch/Manjaro)
sudo pacman -S btrfs-progs

# Check
sudo btrfs check /dev/sdX1

# Mount
sudo mount -t btrfs /dev/sdX1 /mnt
```

---

> Replace `/dev/sdX1` with your actual device (check with `lsblk` or `sudo fdisk -l`).
