---
tags: ["shell-linux", "system", "wifi", "driver", "network"]
---
# Fix Wi-Fi Adapter Driver (Linux)

Diagnoses a missing or broken Wi-Fi driver, installs it from source via DKMS, and applies power management fixes.

Paste and run directly in the terminal — no file needed.

## Diagnose

```bash
# Check USB wireless adapters
lsusb | grep -i wireless

# Check PCI wireless adapters
lspci | grep -i wireless

# Detailed network hardware info
sudo lshw -C network

# Current Wi-Fi radio status
nmcli radio wifi
```

---

## Install driver from source (example: rtw88 / 8821cu)

```bash
# Install build dependencies
sudo apt install dkms build-essential git -y

# Remove the broken module if loaded
sudo rmmod rtw_8821cu

# Clone and install the updated driver
git clone https://github.com/morrownr/8821cu-20210916.git
cd 8821cu-20210916
sudo ./install-driver.sh

sudo reboot
```

> Replace the repo URL with the one matching your chip. Use `lsusb` to identify the chip (e.g., `RTL8821CU`, `MT7601U`).

---

## Disable power management (fixes random disconnects)

```bash
echo "options 8821cu rtw_power_mgnt=0 rtw_lps_level=0 rtw_dynamic_agg_enable=0" | \
  sudo tee /etc/modprobe.d/8821cu.conf

sudo update-initramfs -u
sudo reboot
```

---

## Force 5 GHz band

```bash
# List available networks
nmcli dev wifi list

# Lock a saved connection to 5 GHz
nmcli connection modify "NETWORK_NAME" 802-11-wireless.band a
nmcli connection up "NETWORK_NAME"
```

---

## Test connection quality

```bash
ping -c 5 8.8.8.8
```
