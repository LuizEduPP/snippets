# Dev Snippets

Practical utility scripts, each documented as Markdown with code, usage examples, and dependencies.

---

## Iconify

Scripts for working with the [Iconify](https://iconify.design) icon API.

| Snippet | Description |
|---------|-------------|
| [List collection icons](python/iconify/list-collection-icons.md) | Lists all icons in a collection via the Iconify API |
| [Validate icons by directory](python/iconify/validate-icons-by-directory.md) | Scans JS/TS files and validates all found Iconify icons |
| [Validate static icon list](python/iconify/validate-static-icon-list.md) | Validates a hardcoded list of icons from any collection |

## Audio

| Snippet | Description |
|---------|-------------|
| [Transcribe audio with Whisper](python/audio/transcribe-audio-whisper.md) | Locally transcribes any audio file to text using OpenAI Whisper (no API key needed) |
| [Play audio files](python/audio/play-audio-python.md) | Plays WAV/MP3 from Python using `simpleaudio` or `pygame` — replacements for `playsound` |
| [Hotkey speech dictation](python/audio/hotkey-dictation-whisper.md) | Records audio on a global keyboard shortcut and transcribes it with Whisper + pynput |

## Images

| Snippet | Description |
|---------|-------------|
| [Crop sprite sheet (interactive)](python/images/crop-sprite-grid.md) | Visual tool to define cut lines on a sprite and export each cell |
| [Batch convert PNG to JPG](python/images/batch-convert-png-to-jpg.md) | Converts every PNG in a folder to JPG using Pillow, handling transparency |

## Files

| Snippet | Description |
|---------|-------------|
| [Extract ZIP and filter files](python/files/extract-zip-filter.md) | Extracts a ZIP with optional extension filter, lists files, and reports directory stats |
| [Merge and deduplicate text files](python/files/merge-text-files.md) | Concatenates multiple text/Markdown files into one, with optional line deduplication |

## Video

| Snippet | Description |
|---------|-------------|
| [Generate video report](python/video/generate-video-report.md) | HTML report with Whisper transcription and OCR per frame |
| [Extract text from video](python/video/transcribe-video-text.md) | Extracts audio from a video and transcribes it to text using Whisper + moviepy |

## Tools

| Snippet | Description |
|---------|-------------|
| [VS Code → Eclipse keybindings](python/tools/vscode-to-eclipse-keybindings.md) | Maps VS Code keybindings to Eclipse `.epf` format |
| [ANTT freight table 2025](python/tools/antt-freight-table-2025.md) | Official 2025 ANTT freight rates by transport type, cargo, and axle count |
| [Generate Wi-Fi QR code](python/tools/generate-wifi-qr.md) | Generates a QR code PNG for Wi-Fi auto-connection (WPA/WPA2, WEP, open, hidden) |
| [requests vs curl](python/tools/requests-vs-curl.md) | Side-by-side equivalents for GET, POST, headers, cookies and TLS skip |
| [G-code post-processing runner](python/tools/gcode-post-processing-runner.md) | Runs a chain of G-code scripts after slicing (anti-elephant foot, retractions, timelapse) |
| [pytest quickstart](python/tools/pytest-quickstart.md) | Minimal pytest setup with fixtures, parametrize, and VS Code test runner config |
| [Download from Google Drive](python/tools/download-from-google-drive.md) | Downloads Google Drive files with `gdown`; includes PyInstaller-compatible path helper |
| [CustomTkinter dark theme](python/tools/customtkinter-dark-theme.md) | Applies dark mode and custom color themes to CustomTkinter desktop apps |
| [Validate IP address and port](python/tools/validate-ip-port.md) | Validates IPv4 format and port range; checks if a TCP port is open via socket |

## System — Linux

| Snippet | Description |
|---------|-------------|
| [List GTK/Qt binaries](shell-linux/system/list-gtk-qt-binaries.md) | Lists `/usr/bin` executables that link against GTK or Qt |
| [Check active themes](shell-linux/system/check-active-themes.md) | Displays active GTK 2/3/4 and Qt5/6 themes from config files |
| [Automount partition on boot](shell-linux/system/automount-partition.md) | Adds a partition to `/etc/fstab` for automatic mounting (NTFS, ext4, exFAT) |
| [Kill process on port](shell-linux/system/kill-process-on-port.md) | Checks and kills the process using a given TCP port via `fuser` |
| [Test IP / port reachability](shell-linux/system/test-ip-port.md) | Tests a host:port with `nc`, PowerShell `Test-NetConnection`, or Python socket |
| [Create AppImage shortcut](shell-linux/system/create-appimage-shortcut.md) | Creates a `.desktop` entry so an AppImage appears in the application menu |
| [Share keyboard with Barrier](shell-linux/system/share-keyboard-barrier.md) | Installs and runs Barrier as a systemd service to share keyboard and mouse over LAN |
| [Find MAC address](shell-linux/system/find-mac-address.md) | Shows interface MACs and ARP table of devices on the local network |
| [Restart Samba](shell-linux/system/restart-samba.md) | Restarts smbd/nmbd, checks status, and validates the config with `testparm` |
| [Schedule URL request with cron](shell-linux/system/schedule-url-cron.md) | Uses crontab + curl to hit a URL on a recurring schedule |
| [Fix partition mount errors](shell-linux/system/fix-mount-errors.md) | Repairs and mounts NTFS, exFAT, ext4, and Btrfs partitions using `ntfsfix`, `fsck`, and `e2fsck` |
| [List and test webcam](shell-linux/system/list-test-webcam.md) | Lists `/dev/video*` devices and tests them with `v4l2-ctl`, `ffplay`, and `ffmpeg` |
| [Clipboard with xclip](shell-linux/system/clipboard-xclip.md) | Copies and pastes text to/from the system clipboard in the terminal |
| [Uninstall Dolphin or Nemo](shell-linux/system/uninstall-file-manager.md) | Purges Dolphin/KDE or Nemo/Cinnamon and cleans orphan packages with `deborphan` |
| [Remote access over LAN](shell-linux/system/remote-access-lan.md) | SSH terminal access and full desktop via RDP (xrdp + Remmina + xfreerdp) |
| [Flatpak commands](shell-linux/system/flatpak-commands.md) | Install, run, override env vars, and fix Wayland display issues for Flatpak apps |
| [Switch Klipper printer config](shell-linux/system/switch-klipper-printer.md) | Swaps the active printer config in Klipper and manages multiple Moonraker instances |
| [Run local LLM with Ollama](shell-linux/system/ollama-local-llm.md) | Installs Ollama, pulls a model, and queries it via CLI or HTTP API |
| [Install Nvidia driver](shell-linux/system/install-nvidia-driver.md) | Detects, installs, or reinstalls the correct Nvidia driver on Ubuntu/Zorin |
| [Uninstall KDE Plasma](shell-linux/system/uninstall-kde-plasma.md) | Purges the KDE Plasma desktop and all related packages from Ubuntu/Zorin |
| [Diff and merge tools](shell-linux/system/diff-merge-tools.md) | Meld, KDiff3, Diffuse, vimdiff — Linux alternatives to WinMerge |
| [Fix Wi-Fi adapter driver](shell-linux/system/fix-wifi-driver.md) | Installs a missing driver from source via DKMS and fixes power management disconnects |
| [Install Fluent KDE theme](shell-linux/system/install-fluent-theme-kde.md) | Installs the Fluent KDE theme with Kvantum support on Arch/Manjaro |
| [Boot USB from GRUB rescue shell](shell-linux/system/grub-boot-usb.md) | Manually boots a USB drive or live ISO from the GRUB command line |
| [Flush DNS cache](shell-linux/system/flush-dns-cache.md) | Clears DNS cache on Linux (systemd-resolved, NetworkManager) and Windows |
| [Test RAM with memtester](shell-linux/system/test-ram-memtester.md) | Runs a memory stress test without rebooting to detect faulty RAM modules |
| [Pacman cleanup (Arch/Manjaro)](shell-linux/system/pacman-cleanup.md) | Removes orphaned packages and clears the pacman cache |
| [Remove Chrome PWA / gnome-shell](shell-linux/system/remove-pwa-chrome.md) | Removes the `chrome-gnome-shell` package and uninstalls Chrome PWA desktop apps |
| [Optimize RAM — ZRAM + swappiness](shell-linux/system/optimize-ram-zram.md) | Enables ZRAM compressed swap and tunes swappiness for better performance |
| [KDE Windows 11 style](shell-linux/system/kde-windows11-style.md) | Applies a Windows 11 look to KDE Plasma using Kvantum and WhiteSur |
| [Install llama-cpp-python (CUDA)](shell-linux/system/install-llama-cpp-cuda.md) | Builds llama-cpp-python with CUDA GPU support for local LLM inference |
| [Fix KDE window borders](shell-linux/system/fix-kde-window-borders.md) | Restores missing window borders and title bars in KDE Plasma |
| [Configure ZSwap](shell-linux/system/configure-zswap.md) | Enables and tunes the ZSwap compressed swap cache via GRUB or sysfs |
| [Set default file manager](shell-linux/system/set-default-file-manager.md) | Changes the default file manager using `xdg-mime` (Dolphin, Nautilus, Thunar, Nemo) |
| [Launch web app as window](shell-linux/system/launch-webapp-as-window.md) | Opens any website as a standalone desktop window using Chromium's `--app` flag |
| [View Tomcat logs](shell-linux/system/view-tomcat-logs.md) | Tails and searches Apache Tomcat logs on Linux and Windows |
| [Format SD card or USB drive](shell-linux/system/format-sd-usb.md) | Formats removable storage as FAT32, exFAT, or ext4 from the terminal |
| [Install FFmpeg](shell-linux/system/install-ffmpeg.md) | Installs FFmpeg on Linux and Windows and verifies the PATH |
| [Screen sharing via PipeWire (KDE)](shell-linux/system/screen-sharing-pipewire-kde.md) | Enables screen sharing in Discord/Meet on Wayland by installing XDG portals |
| [Install KDE Plasma on Ubuntu/Zorin](shell-linux/system/install-kde-plasma-ubuntu.md) | Adds KDE Plasma alongside the existing desktop, selectable at login |

## Files — Shell

| Snippet | Description |
|---------|-------------|
| [Reset CSS files](shell-linux/files/reset-css-files.md) | Overwrites every `.css` file with an empty selector block using the filename |
| [Collect and flatten files](shell-linux/files/collect-and-flatten-files.md) | Concatenates all `.py` files into a single timestamped file, one line per file |
| [Extract ZIP without subfolders](shell-linux/files/extract-zip-flat.md) | Extracts all files from a ZIP into a flat directory, stripping folder structure |
| [Move hidden files](shell-linux/files/move-hidden-files.md) | Moves dotfiles and hidden folders included when `mv *` alone would miss them |
| [Auto-populate commit message (hook)](shell-linux/files/git-commit-msg-hook.md) | `prepare-commit-msg` hook that pre-fills branch name and staged file list |
| [Download m3u8 stream with FFmpeg](shell-linux/files/download-m3u8-ffmpeg.md) | Saves an HLS playlist or live stream as a single MP4 via FFmpeg remux |
| [Extract JSON keys with jq](shell-linux/files/extract-json-keys-jq.md) | Lists, sorts, and exports object keys from a JSON file using `jq` |
| [Find and delete files by time](shell-linux/files/find-delete-by-time.md) | Deletes files modified before a specific time today; counts files by extension |
| [Concatenate videos with FFmpeg](shell-linux/files/concatenate-videos-ffmpeg.md) | Merges multiple video clips into one file using FFmpeg concat demuxer |
| [Create timelapse from images](shell-linux/files/create-timelapse-ffmpeg.md) | Combines a folder of JPG/PNG frames into a timelapse MP4 with FFmpeg |

## Android — Shell

| Snippet | Description |
|---------|-------------|
| [ADB logcat](shell-linux/android/adb-logcat.md) | Stream Android device logs with tag, level, and package filters |
| [Install APK via ADB](shell-linux/android/install-apk-adb.md) | Installs an APK directly from the computer to a connected device |
| [Mirror screen with scrcpy](shell-linux/android/mirror-screen-scrcpy.md) | Displays and controls the Android screen on the PC via USB or Wi-Fi |
| [Manage files via ADB](shell-linux/android/manage-files-adb.md) | Lists, pulls, pushes, and deletes files on a connected Android device |
| [Control broken screen via ADB](shell-linux/android/control-broken-screen-adb.md) | Mirrors display with scrcpy and unlocks/types using `adb shell input` |
| [Reset clock via ADB](shell-linux/android/reset-clock-adb.md) | Re-enables auto time sync or sets the clock manually via `adb shell settings` |
| [Install Android Studio (Manjaro)](shell-linux/android/install-android-studio.md) | Installs Android Studio via AUR or Flatpak and sets up the SDK and KVM emulator |
| [Reboot to recovery or fastboot](shell-linux/android/reboot-recovery-fastboot.md) | `adb reboot recovery/bootloader`, `fastboot -w`, and sideload commands |
| [Flash Android firmware partitions](shell-linux/android/flash-android-firmware.md) | Flashes boot/system/vendor/vbmeta with `fastboot flash` to fix bootloops or failed updates |
| [Enable immersive mode via ADB](shell-linux/android/enable-immersive-mode-adb.md) | Forces full-screen mode (hides system bars) on any device without root |
| [Connect device via Wi-Fi (ADB)](shell-linux/android/adb-connect-wifi.md) | Switches ADB to TCP/IP mode for wireless debugging without a cable |
| [Install Magisk (root)](shell-linux/android/install-magisk.md) | Roots a device by patching `boot.img` or flashing Magisk via TWRP |
| [Fix Wi-Fi "No Internet" — LineageOS](shell-linux/android/fix-captive-portal-adb.md) | Disables Android's captive portal check that marks connected Wi-Fi as "No internet" |

## VS Code — Shell

| Snippet | Description |
|---------|-------------|
| [Restore extensions](shell-linux/vscode/restore-extensions.md) | Reinstalls VS Code extensions from a hardcoded list |
| [Register vscode:// URL handler](shell-linux/vscode/register-vscode-url-handler.md) | Registers the `vscode://` protocol on Linux (and Windows) so file links open in the editor |
| [Install VSCodium](shell-linux/vscode/install-vscodium.md) | Installs the privacy-focused, telemetry-free VS Code fork on Linux/macOS |

## System — Windows

| Snippet | Description |
|---------|-------------|
| [Kill process on port](shell-windows/kill-process-on-port.md) | Finds and kills the process using a given port via `netstat` + `taskkill` |
| [Change user password](shell-windows/change-user-password.md) | Lists local users and changes a password via `net user` (requires admin) |
| [Access WSL filesystem](shell-windows/access-wsl-filesystem.md) | Opens the WSL Linux filesystem from Explorer (`\\wsl$\`) and PowerShell |
| [View FortiClient VPN logs](shell-windows/view-forticlient-logs.md) | Tails and searches FortiClient log files on Windows with PowerShell |

---

## License

MIT
