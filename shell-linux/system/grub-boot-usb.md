---
tags: ["shell-linux", "system", "grub", "boot", "usb"]
---
# Boot USB from GRUB Rescue Shell

Manually boots a USB drive or live ISO from the GRUB command line when the bootloader menu fails to list it.

Paste and run directly in the terminal — no file needed.

## Command

### List available disks and partitions

```grub
ls
```

```grub
ls (hd1,gpt1)/
```

> `hd0` = first disk, `hd1` = second disk (usually the USB). `gpt1` / `msdos1` = first partition.

### Boot a Linux live USB (Ubuntu/Debian ISO)

```grub
set root=(hd1,msdos1)
linux /casper/vmlinuz boot=casper quiet splash ---
initrd /casper/initrd
boot
```

### Boot via chainloader (MBR-style USB)

```grub
chainloader (hd1)+1
boot
```

### Boot via EFI chainloader

```grub
set root=(hd1,gpt1)
chainloader /EFI/BOOT/BOOTX64.EFI
boot
```

---

## Tips

- Use `ls (hdX,gptY)/` to browse the filesystem and confirm the path before booting.
- If the USB was created with Ventoy, the EFI path is usually `/EFI/BOOT/BOOTX64.EFI` on `gpt1`.
- Press **Tab** in the GRUB shell to autocomplete paths.
