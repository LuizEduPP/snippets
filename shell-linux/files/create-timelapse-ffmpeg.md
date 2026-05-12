---
tags: ["shell-linux", "files", "ffmpeg", "video", "timelapse"]
---
# Create Timelapse from Images (FFmpeg)

Combines a folder of images (JPG/PNG) into a timelapse MP4 video using FFmpeg. Ideal for 3D printer timelapses, dashcam frames, or stop-motion captures.

Paste and run directly in the terminal — no file needed.

## Command

### From a glob pattern (all JPGs in current folder)

```bash
ffmpeg -r 30 \
  -pattern_type glob \
  -i "*.jpg" \
  -s:v 1920x1080 \
  -c:v libx264 \
  -crf 17 \
  -pix_fmt yuv420p \
  output.mp4
```

- `-r 30` → 30 FPS (adjust for desired speed)
- `-crf 17` → quality (lower = better; 17–23 is good)
- `-s:v 1920x1080` → output resolution (optional)

### From a numbered sequence (`frame-0001.jpg`, `frame-0002.jpg`, …)

```bash
ffmpeg -framerate 30 \
  -i frame-%04d.jpg \
  -c:v libx264 \
  -pix_fmt yuv420p \
  output.mp4
```

### From a text file list (custom order)

```bash
ls -1v *.jpg | while read f; do printf "file '%s'\n" "$f"; done > list.txt
ffmpeg -r 30 -f concat -safe 0 -i list.txt -c:v libx264 -pix_fmt yuv420p output.mp4
```

---

## Rename images to a numbered sequence first

### JPG files

```bash
a=1; for f in *.jpg; do mv "$f" "$(printf "frame-%04d.jpg" $a)"; ((a++)); done
```

### PNG files

```bash
a=1; for f in *.png; do mv "$f" "$(printf "frame-%04d.png" $a)"; ((a++)); done
```

### Verify the sequence

```bash
ls -1 frame-*.jpg | head -10
```

---

## Notes

- `-r 1` = 1 FPS (1 image per second). Good for very long timelapses.
- Add `-vf "scale=trunc(iw/2)*2:trunc(ih/2)*2"` if you get a "width not divisible by 2" error.
- Use `-crf 23` for smaller file size, `-crf 15` for higher quality archiving.
