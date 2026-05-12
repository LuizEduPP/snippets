---
tags: ["shell-linux", "android", "adb", "screen"]
---
# Control Android with Broken Screen (ADB)

Mirrors and controls an Android device when the screen is cracked or unresponsive. Also covers unlocking the screen via ADB input commands.

Paste and run directly in the terminal — no file needed.

## Command

### Check device is connected

```bash
adb devices
```

### Mirror and control the screen on PC

```bash
scrcpy
```

Install scrcpy if needed:

```bash
sudo pacman -S scrcpy   # Arch/Manjaro
sudo apt install scrcpy # Debian/Ubuntu
```

---

## Unlock the screen via ADB (when touch is unresponsive)

### Type a PIN or password

```bash
adb shell input text 1234
```

### Press Enter / confirm

```bash
adb shell input keyevent 66
```

### Wake up the screen

```bash
adb shell input keyevent 26
```

### Swipe up to dismiss lock screen

```bash
adb shell input swipe 540 1600 540 800
```

> Adjust the coordinates based on your screen resolution. Format: `swipe x1 y1 x2 y2`.
