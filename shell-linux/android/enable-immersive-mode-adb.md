---
tags: ["shell-linux", "android", "adb", "immersive"]
---
# Enable Immersive / Full-Screen Mode via ADB

Forces an Android device into immersive mode (hides navigation bar and status bar) using `adb shell settings`. Useful for kiosks, digital signage, and locked-down devices.

Paste and run directly in the terminal — no file needed.

## Command

### Enable immersive mode for all apps

```bash
adb shell settings put global policy_control immersive.full=*
```

### Enable only for a specific app

```bash
adb shell settings put global policy_control immersive.full=com.your.app
```

### Disable (restore system UI)

```bash
adb shell settings put global policy_control null
```

---

## Verify it's active

```bash
adb shell settings get global policy_control
```

---

## Notes

- Works on Android 4.4+ (KitKat and above).
- Does **not** require root.
- The device reverts to normal after reboot unless you add it to `settings.db` or use an MDM profile.
- For permanent kiosk lockdown, combine with `adb shell am start --lock-task`.
