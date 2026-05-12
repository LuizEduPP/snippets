# Project Seven — Shell & Python Snippets

A curated collection of shell and Python snippets organized by domain. Each file includes a breakdown of how the command or script works internally, not just the command itself.

---

## 📁 Structure

```
/
├── android/      # ADB, Fastboot, Scrcpy, Magisk
├── dev-tools/    # Git, VSCode, pytest, gcode, Klipper, Ollama
├── files/        # ZIP extraction, file search, JSON parsing, WSL filesystem
├── media/        # FFmpeg, Whisper transcription, image conversion, OCR
├── network/      # Port testing, DNS, Wi-Fi QR, MAC address, Samba
├── system/       # KDE, drivers, partitions, RAM, AppImage, ZRAM
└── web-apis/     # Iconify, Google Drive, HTTP requests
```

---

## 🤖 android

| File | Description |
|------|-------------|
| [adb-connect-wifi.md](android/adb-connect-wifi.md) | Connect to an Android device via ADB over Wi-Fi |
| [adb-logcat.md](android/adb-logcat.md) | Filter and read Android system logs with logcat |
| [control-broken-screen-adb.md](android/control-broken-screen-adb.md) | Control an Android device with a broken screen using ADB |
| [enable-immersive-mode-adb.md](android/enable-immersive-mode-adb.md) | Enable full-screen immersive mode via ADB |
| [fix-captive-portal-adb.md](android/fix-captive-portal-adb.md) | Fix captive portal detection issues on Android |
| [flash-android-firmware.md](android/flash-android-firmware.md) | Flash firmware partitions using Fastboot |
| [install-android-studio.md](android/install-android-studio.md) | Install Android Studio on Linux |
| [install-apk-adb.md](android/install-apk-adb.md) | Install APK files directly onto a device via ADB |
| [install-magisk.md](android/install-magisk.md) | Root an Android device using Magisk |
| [manage-files-adb.md](android/manage-files-adb.md) | Push and pull files between PC and Android using ADB |
| [mirror-screen-scrcpy.md](android/mirror-screen-scrcpy.md) | Mirror and control an Android screen from a PC using scrcpy |
| [reboot-recovery-fastboot.md](android/reboot-recovery-fastboot.md) | Reboot into recovery or fastboot mode via ADB |
| [reset-clock-adb.md](android/reset-clock-adb.md) | Reset the system clock on an Android device via ADB |

---

## 🛠️ dev-tools

| File | Description |
|------|-------------|
| [customtkinter-dark-theme.md](dev-tools/customtkinter-dark-theme.md) | Apply a dark theme to CustomTkinter GUI applications |
| [diff-merge-tools.md](dev-tools/diff-merge-tools.md) | Compare and merge files using diff and merge tools |
| [gcode-post-processing-runner.md](dev-tools/gcode-post-processing-runner.md) | Run post-processing scripts on G-code files for 3D printing |
| [git/git-commit-msg-hook.md](dev-tools/git/git-commit-msg-hook.md) | Enforce commit message format using a Git hook |
| [install-llama-cpp-cuda.md](dev-tools/install-llama-cpp-cuda.md) | Install llama.cpp with CUDA GPU support |
| [ollama-local-llm.md](dev-tools/ollama-local-llm.md) | Run local LLMs using Ollama |
| [pytest-quickstart.md](dev-tools/pytest-quickstart.md) | Quick reference for writing and running Python tests with pytest |
| [switch-klipper-printer.md](dev-tools/switch-klipper-printer.md) | Switch between printer configurations in Klipper |
| [vscode/install-vscodium.md](dev-tools/vscode/install-vscodium.md) | Install VSCodium (open-source VS Code build) |
| [vscode/register-vscode-url-handler.md](dev-tools/vscode/register-vscode-url-handler.md) | Register VS Code as a URL protocol handler |
| [vscode/restore-extensions.md](dev-tools/vscode/restore-extensions.md) | Export and restore VS Code extension lists |
| [vscode/vscode-to-eclipse-keybindings.md](dev-tools/vscode/vscode-to-eclipse-keybindings.md) | Map VS Code keyboard shortcuts to Eclipse equivalents |

---

## 📂 files

| File | Description |
|------|-------------|
| [access-wsl-filesystem-win.md](files/access-wsl-filesystem-win.md) | Access Linux files from Windows and Windows drives from WSL |
| [collect-and-flatten-files.md](files/collect-and-flatten-files.md) | Flatten a codebase into a single file for LLM context pasting |
| [extract-json-keys-jq.md](files/extract-json-keys-jq.md) | Extract and sort JSON object keys using jq |
| [extract-zip-filter.md](files/extract-zip-filter.md) | Extract specific file types from ZIP archives in Python |
| [extract-zip-flat.md](files/extract-zip-flat.md) | Extract a ZIP file stripping internal folder structure |
| [find-delete-by-time.md](files/find-delete-by-time.md) | Find and delete files by modification time using find |
| [merge-text-files.md](files/merge-text-files.md) | Merge multiple text files into a single output |
| [move-hidden-files.md](files/move-hidden-files.md) | Move hidden dot-files between directories |
| [reset-css-files.md](files/reset-css-files.md) | Strip or reset CSS files in bulk |

---

## 🎬 media

| File | Description |
|------|-------------|
| [audio/hotkey-dictation-whisper.md](media/audio/hotkey-dictation-whisper.md) | Voice dictation to text using a hotkey and Whisper |
| [audio/play-audio-python.md](media/audio/play-audio-python.md) | Play audio files from a Python script |
| [audio/transcribe-audio-whisper.md](media/audio/transcribe-audio-whisper.md) | Transcribe audio files to text using Whisper |
| [images/batch-convert-png-to-jpg.md](media/images/batch-convert-png-to-jpg.md) | Batch convert PNG images to JPG format |
| [images/crop-sprite-grid.md](media/images/crop-sprite-grid.md) | Crop individual sprites from a sprite sheet grid |
| [video/concatenate-videos-ffmpeg.md](media/video/concatenate-videos-ffmpeg.md) | Join multiple video files into one using FFmpeg |
| [video/create-timelapse-ffmpeg.md](media/video/create-timelapse-ffmpeg.md) | Create a timelapse video from images using FFmpeg |
| [video/download-m3u8-ffmpeg.md](media/video/download-m3u8-ffmpeg.md) | Download HLS/M3U8 stream videos using FFmpeg |
| [video/generate-video-report.md](media/video/generate-video-report.md) | Generate an HTML report from a video with Whisper and OCR |
| [video/transcribe-video-text.md](media/video/transcribe-video-text.md) | Extract and transcribe text from video frames |

---

## 🌐 network

| File | Description |
|------|-------------|
| [find-mac-address.md](network/find-mac-address.md) | Find the MAC address of a network interface |
| [fix-wifi-driver.md](network/fix-wifi-driver.md) | Diagnose and fix Wi-Fi driver issues on Linux |
| [flush-dns-cache.md](network/flush-dns-cache.md) | Flush the local DNS resolver cache |
| [forticlient-logs-win.md](network/forticlient-logs-win.md) | Access and read FortiClient VPN logs on Windows |
| [generate-wifi-qr.md](network/generate-wifi-qr.md) | Generate a QR code for Wi-Fi credentials |
| [kill-process-on-port-linux.md](network/kill-process-on-port-linux.md) | Kill a process occupying a specific port on Linux |
| [kill-process-on-port-win.md](network/kill-process-on-port-win.md) | Kill a process occupying a specific port on Windows |
| [remote-access-lan.md](network/remote-access-lan.md) | Set up remote desktop or SSH access on a LAN |
| [requests-vs-curl.md](network/requests-vs-curl.md) | Compare Python requests vs curl for HTTP operations |
| [restart-samba.md](network/restart-samba.md) | Restart the Samba file sharing service |
| [schedule-url-cron.md](network/schedule-url-cron.md) | Schedule HTTP requests using cron |
| [test-ip-port.md](network/test-ip-port.md) | Test connectivity to an IP address and port |
| [validate-ip-port.md](network/validate-ip-port.md) | Validate IP address format and test TCP port reachability |

---

## 💻 system

| File | Description |
|------|-------------|
| [automount-partition.md](system/automount-partition.md) | Auto-mount a disk partition at boot using fstab |
| [change-user-password.md](system/change-user-password.md) | Change a Linux user password via terminal |
| [change-user-password-win.md](system/change-user-password-win.md) | Change a Windows local account password via CMD |
| [check-active-themes.md](system/check-active-themes.md) | List currently active GTK/Qt themes |
| [clipboard-xclip.md](system/clipboard-xclip.md) | Read and write the clipboard using xclip |
| [configure-zswap.md](system/configure-zswap.md) | Enable and configure zswap compressed swap cache |
| [create-appimage-shortcut.md](system/create-appimage-shortcut.md) | Create a .desktop shortcut for an AppImage |
| [fix-kde-window-borders.md](system/fix-kde-window-borders.md) | Fix missing or invisible window borders in KDE Plasma |
| [fix-mount-errors.md](system/fix-mount-errors.md) | Diagnose and fix partition mount errors |
| [flatpak-commands.md](system/flatpak-commands.md) | Common Flatpak package management commands |
| [format-sd-usb.md](system/format-sd-usb.md) | Format SD cards and USB drives from the terminal |
| [grub-boot-usb.md](system/grub-boot-usb.md) | Configure GRUB to boot from a USB device |
| [install-ffmpeg.md](system/install-ffmpeg.md) | Install FFmpeg on Linux |
| [install-fluent-theme-kde.md](system/install-fluent-theme-kde.md) | Install the Fluent theme on KDE Plasma |
| [install-kde-plasma-ubuntu.md](system/install-kde-plasma-ubuntu.md) | Install KDE Plasma on Ubuntu |
| [install-nvidia-driver.md](system/install-nvidia-driver.md) | Install NVIDIA proprietary drivers on Linux |
| [kde-windows11-style.md](system/kde-windows11-style.md) | Style KDE Plasma to look like Windows 11 |
| [launch-webapp-as-window.md](system/launch-webapp-as-window.md) | Launch a web app as a standalone desktop window |
| [list-gtk-qt-binaries.md](system/list-gtk-qt-binaries.md) | List installed GTK and Qt application binaries |
| [list-test-webcam.md](system/list-test-webcam.md) | List and test connected webcams |
| [optimize-ram-zram.md](system/optimize-ram-zram.md) | Enable and configure ZRAM for RAM compression |
| [pacman-cleanup.md](system/pacman-cleanup.md) | Clean up the pacman package cache on Arch Linux |
| [remove-pwa-chrome.md](system/remove-pwa-chrome.md) | Remove PWA shortcuts created by Chrome/Chromium |
| [screen-sharing-pipewire-kde.md](system/screen-sharing-pipewire-kde.md) | Enable screen sharing over PipeWire in KDE |
| [set-default-file-manager.md](system/set-default-file-manager.md) | Set the default file manager application |
| [share-keyboard-barrier.md](system/share-keyboard-barrier.md) | Share keyboard and mouse across machines using Barrier |
| [test-ram-memtester.md](system/test-ram-memtester.md) | Test RAM stability using memtester |
| [uninstall-file-manager.md](system/uninstall-file-manager.md) | Uninstall a file manager without breaking the desktop |
| [uninstall-kde-plasma.md](system/uninstall-kde-plasma.md) | Uninstall KDE Plasma from Ubuntu |
| [view-tomcat-logs.md](system/view-tomcat-logs.md) | View and filter Apache Tomcat server logs |

---

## 🌍 web-apis

| File | Description |
|------|-------------|
| [antt-freight-table-2025.md](web-apis/antt-freight-table-2025.md) | Fetch and parse the ANTT freight reference table |
| [download-from-google-drive.md](web-apis/download-from-google-drive.md) | Download files from Google Drive using gdown |
| [list-collection-icons.md](web-apis/list-collection-icons.md) | List all icons from an Iconify collection |
| [validate-icons-by-directory.md](web-apis/validate-icons-by-directory.md) | Validate component icon attributes against the Iconify API |
| [validate-static-icon-list.md](web-apis/validate-static-icon-list.md) | Validate a static list of icon names against Iconify |
