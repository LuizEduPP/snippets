---
tags: ["bash", "system", "nvidia", "driver", "install"]
---
# Install / Reinstall Nvidia Driver (Ubuntu / Zorin)

Detects the recommended proprietary hardware interfaces, purges broken installations, and injects the correct Nvidia drivers into the kernel module tree.

## 🛠️ How it works under the hood

1. **`ubuntu-drivers` utility**: A canonical script that parses PCI vendor data, matches the local hardware to the upstream driver repositories, and assigns the correct DKMS packages automatically.
2. **`apt remove --purge`**: Video drivers hook deeply into X11/Wayland. A simple remove leaves configuration files scattered, causing bootloops. Purging ensures the entire dependency chain is eradicated before reinstalling headers.

---

## 🚀 Usage Guide

### 1. Identify Hardware Requirements
```bash
# Scan PCI blocks and check remote registries
sudo ubuntu-drivers devices
```

### 2. Standard Installation Route
```bash
# Allow the script to resolve and inject the recommended package
sudo ubuntu-drivers autoinstall

# Or enforce a specific kernel module version manually
sudo apt install nvidia-driver-550
```

### 3. Emergency Purge and Reinstall (Fix Broken Drivers)
If the screen is tearing or failing to boot into a graphical session, wipe the module tree.
```bash
# Wipe all old Nvidia config files from the system
sudo apt remove --purge '^nvidia-.*'
sudo apt autoremove
sudo apt clean

# Update headers and pull clean packages
sudo apt update && sudo apt upgrade -y
sudo apt install nvidia-driver-550
sudo reboot
```

### 4. Verify Kernel Load
```bash
# Verify the kernel module is communicating with the GPU
nvidia-smi
```
