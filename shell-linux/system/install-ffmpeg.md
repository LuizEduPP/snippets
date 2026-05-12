---
tags: ["shell-linux", "system", "ffmpeg", "install"]
---
# Install FFmpeg (Linux / Windows)

Installs FFmpeg system-wide and verifies the installation. Required by many tools that throw `spawn ffmpeg ENOENT` or `Cannot find ffmpeg`.

Paste and run directly in the terminal — no file needed.

## Command

### Linux — Debian/Ubuntu

```bash
sudo apt update && sudo apt install ffmpeg
```

### Linux — Arch/Manjaro

```bash
sudo pacman -S ffmpeg
```

### Linux — Fedora

```bash
sudo dnf install ffmpeg
```

### Windows — Chocolatey

```powershell
choco install ffmpeg
```

### Windows — Scoop

```powershell
scoop install ffmpeg
```

### Windows — Manual

Download from [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html), extract, and add the `bin/` folder to your system `PATH`.

---

## Verify the installation

```bash
ffmpeg -version
which ffmpeg       # Linux/macOS
where ffmpeg       # Windows
```

---

## Set a custom path in Node.js (fluent-ffmpeg)

```javascript
const ffmpeg = require("fluent-ffmpeg");

ffmpeg.setFfmpegPath("/usr/bin/ffmpeg");
ffmpeg.setFfprobePath("/usr/bin/ffprobe");
```
