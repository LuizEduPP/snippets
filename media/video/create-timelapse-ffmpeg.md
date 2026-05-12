---
tags: ["linux", "media", "ffmpeg", "video", "timelapse"]
---
# Create a Timelapse from Images (FFmpeg)

This translates an entire folder containing hundreds of raw images (like from a dashcam, a 3D Print octoprint dump, or a stop-motion photography session) and compresses it into a high-quality, timed MP4 video.

## 🛠️ How it works under the hood

1. **`-r 30` / `-framerate 30`**: Dictates the final frames per second. Higher values mean the timelapse is faster/shorter.
2. **`-pattern_type glob -i "*.jpg"`**: Directs ffmpeg to ingest every `.jpg` file in the folder indiscriminately rather than passing each filename.
3. **`-c:v libx264`**: Enforces the universal H.264 MP4 encoding logic, guaranteeing playback on almost any device globally.
4. **`-crf 17`**: Constant Rate Factor. Lower numbers = Higher quality and larger file size. A standard acceptable range is **17–23**.
5. **`-pix_fmt yuv420p`**: Enforces the 4:2:0 chroma subsampling profile across pixels, which is mandatory requirement for most phone screens and macOS players to interpret the color depths without throwing errors.

---

## 🚀 Usage Guide 

Ensure your terminal's current directory is the folder holding the raw files.

### 1. Simple Drop-and-Grab Method (Glob)
This captures all files matching the `.jpg` extension regardless of their filenames.

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
*(Note: Remove the `-s:v 1920x1080` if you do not want to force resolution scaling ).*

### 2. Strict Sequencing Mode
If you need guaranteed strict ordering, use the numbering syntax. Files **must** be named like `frame-0001.jpg`, `frame-0002.jpg`, etc.

```bash
ffmpeg -framerate 30 \
 -i frame-%04d.jpg \
 -c:v libx264 \
 -pix_fmt yuv420p \
 output.mp4
```
*(`%04d` specifies a 4-digit zero-padded number structure).*

---

## 💡 Pre-processing Utilities

If your files are randomly named hashes and you want to rename them sequentially to fit the "Strict Sequencing Mode" above:

### Bulk rename JPGs sequentially:
```bash
a=1; for f in *.jpg; do mv "$f" "$(printf "frame-%04d.jpg" $a)"; ((a++)); done
```

### Verification Quick Check:
Validates the first ten segments generated:
```bash
ls -1 frame-*.jpg | head -10
```

## 🐛 Troubleshooting

Error: `width not divisible by 2`
H.264 rendering strictly requires total resolutions to be divisible by even numbers (no odd-pixel widths allowed). Inject this fix into your command:
```bash
-vf "scale=trunc(iw/2)*2:trunc(ih/2)*2"
```
