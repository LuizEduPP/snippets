---
tags: ["shell-linux", "system", "format", "usb", "sd-card"]
---
# Format SD Card or USB Drive (Linux)

Formats a storage device as FAT32 or exFAT from the Linux terminal. Used for SD cards, USB drives, and portable storage.

Paste and run directly in the terminal — no file needed.

## Command

### Step 1 — identify the device

```bash
lsblk
```

> Find your device (e.g., `/dev/sdb`, `/dev/mmcblk0`). **Double-check before formatting** — wrong device will erase data.

### Step 2 — unmount

```bash
sudo umount /dev/sdX1    # replace sdX1 with your partition
```

### Step 3 — format

#### FAT32 (≤32 GB, max compatibility)

```bash
sudo mkfs.vfat -F 32 /dev/sdX
```

#### exFAT (>32 GB, modern devices)

```bash
sudo apt install exfatprogs    # Debian/Ubuntu
sudo mkfs.exfat /dev/sdX
```

#### ext4 (Linux only)

```bash
sudo mkfs.ext4 /dev/sdX
```

---

## Optional — wipe partition table first

```bash
sudo wipefs -a /dev/sdX
```

---

## Install GParted (GUI alternative)

```bash
sudo apt install gparted -y
gparted
```

---

## Notes

- Format the **device** (`/dev/sdX`), not the partition (`/dev/sdX1`), if you want to replace the partition table.
- To add a label: `sudo mkfs.vfat -F 32 -n "MYCARD" /dev/sdX`
- `lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT` gives a more readable view.
