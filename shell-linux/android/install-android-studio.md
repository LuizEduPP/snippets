---
tags: ["shell-linux", "android", "install"]
---
# Install Android Studio on Manjaro / Arch

Installs Android Studio via the AUR, Flatpak, or official Snap, and sets up the Android SDK.

Paste and run directly in the terminal — no file needed.

## Command

### Option 1 — AUR (pamac)

```bash
pamac build android-studio
```

### Option 2 — AUR (yay)

```bash
yay -S android-studio
```

### Option 3 — Flatpak

```bash
flatpak install flathub com.google.AndroidStudio
flatpak run com.google.AndroidStudio
```

---

## Set up the Android SDK

```bash
# Install SDK tools via pamac
pamac install android-sdk android-sdk-platform-tools android-sdk-build-tools android-tools
```

### Add Android tools to PATH

```bash
# Bash
echo 'export PATH=$PATH:$HOME/Android/Sdk/platform-tools' >> ~/.bashrc
source ~/.bashrc

# Zsh
echo 'export PATH=$PATH:$HOME/Android/Sdk/platform-tools' >> ~/.zshrc
source ~/.zshrc
```

---

## Enable hardware acceleration (KVM) for the emulator

```bash
# Check if CPU supports virtualization
egrep -c '(vmx|svm)' /proc/cpuinfo
# Returns 0 = not supported, 1+ = supported

# Install KVM and libvirt
sudo pamac install qemu-base libvirt virt-manager bridge-utils
sudo systemctl enable --now libvirtd
sudo usermod -aG libvirt $(whoami)
# Log out and back in after this step
```

---

## Launch

```bash
android-studio
# Or
studio.sh
# If UI is broken on Wayland:
studio.sh --no-sandbox
```
