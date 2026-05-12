---
tags: ["shell-linux", "android", "adb", "logcat", "debug"]
---
# Android Logcat (ADB)

Stream real-time Android logs from a connected device or emulator for debugging. Requires ADB in `PATH` and USB debugging enabled on the device.

Paste and run directly in the terminal — no file needed.

## Command

### Stream all logs

```bash
adb logcat
```

### Clear buffer then stream

```bash
adb logcat -c && adb logcat
```

---

## Filters

### By tag (show only a specific component)

```bash
adb logcat -s ReactNative:V
```

Format: `-s <TAG>:<LEVEL>` — levels: `V` verbose, `D` debug, `I` info, `W` warn, `E` error.

### Errors only (all tags)

```bash
adb logcat *:E
```

### By app package (requires the app to be running)

```bash
adb logcat --pid=$(adb shell pidof -s com.yourapp.package)
```

---

## Export logs to file

```bash
adb logcat -d > logs.txt
```

The `-d` flag dumps the current buffer and exits (does not stream).
