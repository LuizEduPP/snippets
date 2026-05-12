---
tags: ["shell-linux", "android", "adb", "clock"]
---
# Reset Android Clock via ADB

Fixes incorrect date/time on an Android device by re-enabling automatic time sync or setting the time manually.

Paste and run directly in the terminal — no file needed.

## Command

### Re-enable automatic time and timezone sync

```bash
adb shell settings put global auto_time 1
adb shell settings put global auto_time_zone 1
adb shell am broadcast -a android.intent.action.TIME_SET
```

### Set time manually (requires root)

Replace the date/time string with the current value.

```bash
adb shell su -c "date -s '2025-06-22 19:45:00'"
adb shell am broadcast -a android.intent.action.TIME_SET
```

### Reboot if the clock still shows wrong after syncing

```bash
adb reboot
```

### Force the system clock to refresh without rebooting (requires root)

```bash
adb shell su -c "pkill com.android.systemui"
```
