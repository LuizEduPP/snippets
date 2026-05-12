---
tags: ["shell-linux", "system", "fstab", "mount", "partition", "ntfs"]
---
# Automount Partition on Boot (fstab)

Configures a partition to mount automatically at startup by adding an entry to `/etc/fstab`. Works with NTFS, ext4, and exFAT.

Paste each block directly in the terminal — no file needed.

---

## Step 1 — Install drivers (if needed)

```bash
# NTFS
sudo pacman -S ntfs-3g      # Arch/Manjaro
sudo apt install ntfs-3g    # Debian/Ubuntu

# exFAT
sudo pacman -S exfatprogs   # Arch/Manjaro
sudo apt install exfat-fuse # Debian/Ubuntu
```

## Step 2 — Create mount point

```bash
sudo mkdir -p /mnt/data
```

## Step 3 — Find the partition UUID

```bash
sudo blkid
```

Look for a line like:
```
/dev/nvme0n1p3: UUID="AABBCCDD11223344" TYPE="ntfs"
```

Or use `lsblk -f` for a tree view:

```bash
lsblk -f
```

## Step 4 — Find your UID and GID

```bash
id
```

## Step 5 — Back up fstab and add the entry

```bash
sudo cp /etc/fstab /etc/fstab.backup
```

Then open fstab:

```bash
sudo nano /etc/fstab
```

Add one of the lines below at the end, replacing the UUID and `/mnt/data` with your values.

### NTFS

```fstab
UUID=66A4025DA402305B  /mnt/data  ntfs-3g  defaults,uid=1000,gid=1000,windows_names,locale=en_US.utf8  0  0
```

### ext4

```fstab
UUID=abc123def456  /mnt/data  ext4  defaults,noatime  0  2
```

### exFAT

```fstab
UUID=xyz789abc  /mnt/data  exfat  defaults,uid=1000,gid=1000  0  0
```

## Step 6 — Test without rebooting

```bash
sudo mount -a
```

No output means success. Verify with:

```bash
mount | grep /mnt/data
```

---

## Common mount options

| Option | Effect |
|--------|--------|
| `uid=1000` | Sets the owner to your user (replace with your UID) |
| `gid=1000` | Sets the group (replace with your GID) |
| `noatime` | Skips updating access timestamps — improves performance |
| `discard` | Enables TRIM for SSDs (ext4 only) |
| `windows_names` | NTFS: avoids filenames that break on Windows |

---

## One-time manual mount (without fstab)

```bash
# NTFS with read/write permissions
sudo mount -t ntfs-3g /dev/sda1 /mnt/data \
  -o umask=022,uid=1000,gid=1000
```

```bash
# Full read/write for current user
sudo mount -t ntfs-3g /dev/sda1 /mnt/data \
  -o umask=000,uid=$(id -u),gid=$(id -g)
```

> Replace `/dev/sda1` with your actual device (check with `lsblk`). Use `umask=022` for standard access, `umask=000` to allow all users full write access.

> **NTFS from hibernated Windows** is mounted read-only. Disable Fast Startup in Windows (Power Options → Turn off fast startup) to fix this.
