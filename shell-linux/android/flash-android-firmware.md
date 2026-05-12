---
tags: ["shell-linux", "android", "fastboot", "firmware", "flash"]
---
# Flash Android Firmware Partitions (fastboot)

Reflashes individual Android partitions from stock firmware files using `fastboot` — useful for fixing bootloops or recovering from failed updates.

Paste and run directly in the terminal — no file needed.

## Command

### Enter fastboot mode

```bash
# From a running device
adb reboot bootloader

# Physical buttons (most devices): hold Volume Down + Power
```

### Verify the device is detected

```bash
fastboot devices
# On Linux, try: sudo fastboot devices
```

### Flash individual partitions

```bash
fastboot flash boot      boot.img
fastboot flash system    system.img
fastboot flash vendor    vendor.img
fastboot flash vbmeta    vbmeta.img --disable-verity --disable-verification
```

### Reboot after flashing

```bash
fastboot reboot
```

---

## Wipe and full restore

```bash
# Wipe all user data
fastboot -w

# Flash all partitions then reboot
fastboot flash boot   boot.img
fastboot flash system system.img
fastboot flash vendor vendor.img
fastboot -w
fastboot reboot
```

---

## Boot a custom recovery temporarily (no permanent flash)

```bash
fastboot boot twrp.img
```

---

## Sideload a ZIP via ADB in recovery

```bash
# Select "Apply update from ADB" in the recovery menu, then:
adb sideload update.zip
```

> Always match firmware to your exact device model and Android version. Flashing wrong partitions can brick the device.
