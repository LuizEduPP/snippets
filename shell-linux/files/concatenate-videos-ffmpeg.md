---
tags: ["shell-linux", "files", "ffmpeg", "video", "concat"]
---
# Concatenate Videos with FFmpeg

Merges multiple video files into a single output file using FFmpeg's concat demuxer. Works with MP4, MKV, and other formats without re-encoding (when codecs match).

Paste and run directly in the terminal — no file needed.

## Command

### Fast concat — same codec, no re-encode

```bash
# Create a list of input files
printf "file '%s'\n" clip1.mp4 clip2.mp4 clip3.mp4 > list.txt

# Merge without re-encoding
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

---

### Re-encode first (required when codecs differ)

```bash
ffmpeg -i clip1.mp4 -c:v libx264 -c:a aac temp1.mp4
ffmpeg -i clip2.mp4 -c:v libx264 -c:a aac temp2.mp4

printf "file '%s'\n" temp1.mp4 temp2.mp4 > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

---

### Concatenate all MP4 files in a folder (alphabetical order)

```bash
ls -1v *.mp4 | while read f; do printf "file '%s'\n" "$f"; done > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

---

### Trim before merging

```bash
# Trim clip1: from 0:10 to 1:30
ffmpeg -ss 00:00:10 -to 00:01:30 -i clip1.mp4 -c copy trimmed1.mp4
```

---

## Notes

- `Error: Output file does not contain any stream` means the clips have different codecs — re-encode first.
- Use `-c copy` when possible — it's instant and lossless.
- `-safe 0` is required if paths contain spaces or special characters.
