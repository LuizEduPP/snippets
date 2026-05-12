---
tags: ["bash", "android", "adb", "screen", "scrcpy"]
---
# Control Android with Broken Screen (ADB)

A set of automated bypass instructions rescuing completely physically shattered or unresponsive Android displays. It bridges internal ADB input simulators dynamically unlocking local pin codes safely prior to launching absolute display mirroring streams entirely ignoring the broken touchscreen interface. ## 🛠️ How it works under the hood

1. **`adb shell input...`**: Android hosts an internal synthetic injection proxy daemon under the hood that translates pure text commands globally into physical hardware button presses or exact touchscreen X/Y coordinates mathematically. 2. **`scrcpy`**: An ultra-low latency C-based bridge executable mapping raw H.264/H.265 video rendering frames directly pushing physical pixels off the device's internal GPU over standard USB interfaces onto the PC desktop window.

---

## ⚡ Setup / Installation

You must possess the visual display mirror utility locally built dynamically:
```bash
# Arch / Manjaro Arrays
sudo pacman -S scrcpy

# Debian / Ubuntu Nodes
sudo apt install scrcpy
```

---

## 🚀 Usage Guide

### Phase 1: Bypassing the Physical Lock Screen
If the touchscreen is shattered globally, you cannot click the GUI. Pass absolute simulated logic synthetically:

```bash
# 1. Simulate pressing the physical power button to wake internal sensors
adb shell input keyevent 26

# 2. Emulate an exact vector finger swipe traversing the Y-axis unlocking standard Android view interfaces
# Syntax: `swipe x1 y1 x2 y2`
adb shell input swipe 540 1600 540 800

# 3. Inject standard text dynamically mapping your PIN digits
adb shell input text 1234

# 4. Trigger the exact Enter key validating the security barrier structurally
adb shell input keyevent 66
```

### Phase 2: Interfacing GUI Architecture locally
Once unlocked definitively, launch the massive video rendering binary payload globally instantiating interactions on the computer window:

```bash
scrcpy
```
