---
tags: ["shell-linux", "android", "scrcpy", "screen", "mirror"]
---
# Mirror Android Screen with scrcpy

Displays and controls an Android device screen on your computer over USB or Wi-Fi.

Paste and run directly in the terminal — no file needed.

## Command

### Install

```bash
# Arch/Manjaro
sudo pacman -S scrcpy

# Debian/Ubuntu
sudo apt install scrcpy
```

### Connect via USB

```bash
scrcpy
```

### Connect via Wi-Fi (same network)

```bash
adb tcpip 5555
adb connect 192.168.1.100:5555
scrcpy
```

Replace `192.168.1.100` with the device IP (found in *Settings → About → IP address*).

---

## Options

| Flag | Effect |
|------|--------|
| `--max-size 1024` | Limit resolution (improves performance) |
| `--record video.mp4` | Record screen to file |
| `--no-control` | View only, no input |
| `--fullscreen` | Open fullscreen |
| `--keyboard=uhid` | Enhanced keyboard input mode |

### Connect to a specific device

```bash
adb devices                # list serial numbers
scrcpy -s be255cda         # use that serial
```
