---
tags: ["shell-linux", "android", "adb", "network", "lineageos"]
---
# Fix LineageOS Wi-Fi "No Internet" (Captive Portal)

Disables Android's captive portal check that marks connected Wi-Fi networks as "No internet access" on custom ROMs or in networks that block Google connectivity checks.

Paste and run directly in the terminal — no file needed.

## Command

### Disable captive portal detection via ADB

```bash
adb shell settings put global captive_portal_mode 0
```

### Re-enable

```bash
adb shell settings put global captive_portal_mode 1
```

### Alternative — disable detection entirely

```bash
adb shell settings put global captive_portal_detection_enabled 0
```

---

### Via Termux (requires root on device)

```bash
su -c "settings put global captive_portal_mode 0"
su -c "settings put global captive_portal_detection_enabled 0"
```

---

## Verify and troubleshoot

```bash
# Check current value
adb shell settings get global captive_portal_mode

# Test basic connectivity
adb shell ping -c 3 8.8.8.8

# Toggle Wi-Fi off/on
adb shell svc wifi disable
adb shell svc wifi enable
```

---

## Notes

- `captive_portal_mode 0` = disabled; `1` = detect but allow; `2` = prompt user.
- On stock Android, consider changing the captive portal URL to use a non-Google endpoint (e.g., Cloudflare's `captiveportal.detectportal.firefox.com`).
- This command survives reboots but may reset after a LineageOS OTA update.
