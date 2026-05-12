---
tags: ["shell-linux", "android", "adb", "wifi"]
---
# Connect Android Device via Wi-Fi (ADB)

Switches ADB from USB to wireless mode so you can debug and run commands over the local network without keeping the cable plugged in.

Paste and run directly in the terminal — no file needed.

## Command

### 1. Connect via USB first, then get the device IP

```bash
adb shell ip route
# Example output: 192.168.1.123 dev wlan0
```

### 2. Switch to TCP/IP mode

```bash
adb tcpip 5555
```

### 3. Unplug the USB cable, then connect over Wi-Fi

```bash
adb connect 192.168.1.123:5555
```

### 4. Verify the connection

```bash
adb devices
# Output: 192.168.1.123:5555  device
```

---

## Disconnect and revert to USB

```bash
adb disconnect 192.168.1.123:5555

# Or disconnect all wireless devices
adb disconnect
```

---

## Troubleshoot

```bash
# Scan for nearby Wi-Fi networks (no root needed)
adb shell cmd wifi list-scan-results

# Show detailed Wi-Fi status
adb shell dumpsys wifi | head -40

# Show Wi-Fi related logs
adb logcat | grep -i wifi
```

> The phone and computer must be on the same Wi-Fi network. The TCP/IP mode resets on reboot — repeat from step 1 each time.
