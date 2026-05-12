---
tags: ["shell-linux", "android", "adb", "apk", "install"]
---
# Install APK via ADB

Installs an Android APK directly from your computer to a connected device or emulator. Requires USB debugging enabled on the device.

Paste and run directly in the terminal — no file needed.

## Command

### Check connected devices

```bash
adb devices
```

Expected output:
```
List of devices attached
be255cda    device
```

If it shows `unauthorized`, accept the permission prompt on the phone.

### Install APK

```bash
adb install -r /path/to/app.apk
```

> `-r` reinstalls over an existing app with the same package ID, keeping its data.

### Install to a specific device (when multiple are connected)

```bash
adb -s be255cda install -r /path/to/app.apk
```

---

## Install ADB

```bash
# Arch/Manjaro
sudo pacman -S android-tools

# Debian/Ubuntu
sudo apt install adb
```
