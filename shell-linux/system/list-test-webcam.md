---
tags: ["shell-linux", "system", "webcam", "v4l2", "ffmpeg"]
---
# List and Test Webcam Devices

Lists available video capture devices and tests them with ffmpeg or ffplay without installing a GUI application.

Paste and run directly in the terminal — no file needed.

## Command

### List video devices

```bash
ls /dev/video*
```

```bash
# Detailed device info
v4l2-ctl --list-devices
```

### Test live preview

```bash
ffplay /dev/video0
```

### Capture a single test frame

```bash
ffmpeg -f v4l2 -i /dev/video0 -vframes 1 test.jpg
```

### Check supported resolutions and formats

```bash
v4l2-ctl --device=/dev/video0 --list-formats-ext
```

### Stream via MJPG (HTTP)

```bash
ffmpeg -f v4l2 -input_format mjpeg -video_size 1280x720 \
  -i /dev/video0 -f mjpeg http://localhost:8080/feed
```

---

## Troubleshooting

### Device permission denied

```bash
# Check group
ls -lah /dev/video0

# Add user to video group
sudo usermod -aG video $USER
# Log out and back in for the group change to apply
```

### Install v4l-utils if missing

```bash
# Arch/Manjaro
sudo pacman -S v4l-utils

# Debian/Ubuntu
sudo apt install v4l-utils
```
