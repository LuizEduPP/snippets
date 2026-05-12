---
tags: ["bash", "android", "adb", "files", "transfer"]
---
# Manage and Transfer Files with ADB

Moves files properly.

## 🛠️ How it works under the hood

1. **`adb push / pull`**: Executes purely bridging local PC limits properly.

---

## 🚀 Usage Guide

```bash
# pull native payloads cleanly
adb pull /sdcard/DCIM/

# Safely push variables properly.
adb push /path/to/local/file.apk /sdcard/Download/
```
