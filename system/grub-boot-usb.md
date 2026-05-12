---
tags: ["bash", "system", "grub", "boot", "usb"]
---
# Boot USB from GRUB Rescue Shell

Bypasses broken bootloader menus manually forcing the kernel to map and boot an external USB drive or live ISO from the raw GRUB prompt.

## 🛠️ How it works under the hood

1. **GRUB variables (`set root=`)**: GRUB reads raw disk coordinates before the kernel exists. MBR styles map as `msdos1`, while modern UEFI maps as `gpt1`.
2. **`chainloader` / `linux` Payload**: Depending on the boot architecture, GRUB either passes execution completely to the `vmlinuz` raw kernel payload directly, or chain-loads execution control fully to a `.EFI` secondary bootloader inside the USB drive.

---

## 🚀 Usage Guide

### 1. Map connected hardware blocks
```bash
# List all physical and logical drives (Shows hd0, hd1...)
ls

# Check inside a target drive to confirm its contents
ls (hd1,gpt1)/
```

### 2. Boot a Linux target (Casper/vmlinuz)
This specifically executes standard debian-based live ISO roots dynamically.
```bash
# Set default root pointer
set root=(hd1,msdos1)

# Pass kernel limits
linux /casper/vmlinuz boot=casper quiet splash ---

# Render pre-boot filesystem
initrd /casper/initrd

# Execute kernel switch
boot
```

### 3. Boot via EFI secondary bootloader (Ventoy/Windows)
```bash
# Point GRUB root to the external drive
set root=(hd1,gpt1)

# Hand over limits entirely to the external bootloader payload
chainloader /EFI/BOOT/BOOTX64.EFI

# Execute kernel switch
boot
```
