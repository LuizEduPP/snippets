---
tags: ["shell-linux", "android", "fastboot", "recovery", "reboot"]
---
# Reboot to Recovery or Fastboot (ADB)

Reboots a connected Android device into recovery, fastboot, or performs a factory reset via ADB and fastboot commands.

Paste and run directly in the terminal — no file needed.

## Command

### Check connected devices

```bash
adb devices
fastboot devices
```

> If `fastboot devices` returns empty on Linux, try: `sudo fastboot devices`

### Reboot to recovery

```bash
adb reboot recovery
```

### Reboot to bootloader (fastboot mode)

```bash
adb reboot bootloader
```

---

## Fastboot operations

### Factory reset (wipe all data)

```bash
fastboot -w
```

### Restart back to the system

```bash
fastboot reboot
```

### Restart to recovery from fastboot

```bash
fastboot reboot recovery
```

### Check device info (some OEMs)

```bash
fastboot oem device-info
```

---

## Sideload a ZIP in recovery

```bash
# In recovery, select "Apply update from ADB", then on the computer:
adb sideload update.zip
```

---

> Physical button combo to enter recovery (no ADB needed):  
> **Most Android devices**: hold **Volume Up + Power** for 15–20 seconds until the menu appears.
