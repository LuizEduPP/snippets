---
tags: ["shell-linux", "android", "adb", "files"]
---
# Manage Files via ADB

Lists, copies, and transfers files between a computer and an Android device using ADB shell commands.

Paste and run directly in the terminal — no file needed.

## Command

### Open interactive shell on the device

```bash
adb shell
```

### List files

```bash
# Internal storage root
adb shell ls /sdcard/

# Specific folder
adb shell ls -la /sdcard/Download/

# Save listing to a file on the PC
adb shell ls /sdcard/ > listing.txt
```

### Copy from device to PC

```bash
# Single file
adb pull /sdcard/file.zip

# Single file to specific destination
adb pull /sdcard/file.zip ~/Desktop/

# Entire folder
adb pull /sdcard/DCIM/
```

### Copy from PC to device

```bash
adb push /path/to/local/file.apk /sdcard/Download/
```

### Delete a file on the device

```bash
adb shell rm /sdcard/Download/file.zip
```

---

> Requires USB debugging enabled. Run `adb devices` first to confirm the device is connected and authorized.
