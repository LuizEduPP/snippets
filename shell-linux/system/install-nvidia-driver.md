---
tags: ["shell-linux", "system", "nvidia", "driver", "install"]
---
# Install / Reinstall Nvidia Driver (Ubuntu / Zorin)

Detects the recommended Nvidia driver, removes broken installations, and installs the correct version.

Paste and run directly in the terminal — no file needed.

## Command

### Check available drivers

```bash
sudo ubuntu-drivers devices
```

### Install the recommended driver automatically

```bash
sudo ubuntu-drivers autoinstall
```

### Or install a specific version

```bash
sudo apt install nvidia-driver-550
```

### Remove a broken or conflicting Nvidia installation

```bash
sudo apt remove --purge '^nvidia-.*'
sudo apt autoremove
sudo apt clean
```

### Reinstall after cleanup

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nvidia-driver-550
sudo reboot
```

### Verify the driver is loaded after reboot

```bash
nvidia-smi
```

> Replace `550` with the version shown by `ubuntu-drivers devices`. On Arch/Manjaro use `sudo mhwd -i pci video-nvidia` instead.
