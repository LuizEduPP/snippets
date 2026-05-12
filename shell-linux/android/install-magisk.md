---
tags: ["shell-linux", "android", "magisk", "root", "twrp"]
---
# Install Magisk (Root) via Fastboot or TWRP

Roots an Android device by patching the `boot.img` with Magisk and flashing it via fastboot, or by flashing the Magisk ZIP through TWRP recovery.

Paste and run directly in the terminal — no file needed.

## Method 1 — Patch boot.img via Magisk App (recommended)

```
1. Copy the stock boot.img to the device storage
2. Open Magisk App → Install → Select and Patch a File
3. Select boot.img → Magisk saves patched file in Downloads/
4. Copy the patched file back to the PC
```

```bash
# Flash the patched boot image
fastboot flash boot magisk_patched_*.img
fastboot reboot
```

---

## Method 2 — Flash via TWRP recovery

```bash
# Reboot to TWRP
adb reboot recovery
```

```
In TWRP: Install → Select magisk.zip → Swipe to confirm → Reboot
```

---

## Method 3 — Boot (temp root, no flash)

```bash
fastboot boot magisk_patched.img
```

> Runs Magisk without permanently writing to the partition. Reverts on next reboot.

---

## Verify root after reboot

```bash
adb shell su -c "id"
# Expected: uid=0(root)
```

---

## Notes

- Always use the stock `boot.img` that matches your exact firmware version.
- Magisk preserves OTA update compatibility when using the "Direct Install" method.
- SafetyNet/Play Integrity may require additional modules (e.g., `shamiko`, `playintegrityfix`).
