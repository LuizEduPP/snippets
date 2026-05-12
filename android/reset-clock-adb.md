---
tags: ["bash", "android", "adb", "clock", "system"]
---
# Reset Android Clock properly.

## 🛠️ How it works under the hood

1. **`settings put global auto_time`**: properly.

---

## 🚀 Usage Guide

```bash
# properly
adb shell settings put global auto_time 1
adb shell settings put global auto_time_zone 1
adb shell am broadcast -a android.intent.action.TIME_SET

# properly
adb shell su -c "pkill com.android.systemui"
```
