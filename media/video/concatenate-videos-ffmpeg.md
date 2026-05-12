---
tags: ["linux", "media", "ffmpeg", "video", "merge"]
---
# Concatenate Videos with FFmpeg

This merges multiple split video files (like segments of a presentation) into one giant continuous file using FFmpeg's `concat` demuxer. It bypasses the need for heavy GUI video editors (like Premiere or Resolve) and takes mere seconds if the clips share the exact same codec structure.

## 🛠️ How it works under the hood

1. **`list.txt`**: Generates a standard text manifest telling `ffmpeg` what files to look for, utilizing `printf` mapping logic. `ffmpeg` expects a strict format like `file 'clip1.mp4'`.
2. **`-f concat`**: Forces ffmpeg into its specialized concatenation mode path parser rather than treating elements as layered streams.
3. **`-safe 0`**: Prevents `ffmpeg` from rejecting video files based on spaces or strange characters present in the OS's file path strings.
4. **`-c copy`**: Skips all re-encoding entirely. It surgically stitches the data bytes together. ---

## 🚀 Usage Guide

For the fastest merge, ensure all your video clips have matching codecs and resolutions!

### 1. The Fast Native Merge (Lossless)
This assumes your videos match encodings. This merges `clip1.mp4` and `clip2.mp4`:

```bash
# 1. Create a mapped manifest text file
printf "file '%s'\n" clip1.mp4 clip2.mp4 > list.txt

# 2. Merge them based on the text file map
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

### 2. Auto-Merge A Full Directory Alphabetically
If you have 50 split fragments sequentially named (like `part-1.mp4`, `part-2.mp4`):

```bash
ls -1v *.mp4 | while read f; do printf "file '%s'\n" "$f"; done > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```
*(The `-1v` flag on `ls` forces proper natural number sorting (so `part-10` comes after `part-9`, not after `part-1`)).*

### 3. Re-encode Merge Fix (When Codecs Fail)
If the above commands throw `Error: Output file does not contain any stream`, it proves the videos were packaged differently and cannot be losslessly mashed together. You must re-encode them all first to a universal baseline (like `libx264`) before making the list:

```bash
# Force universal baselines
ffmpeg -i clip1.mkv -c:v libx264 -c:a aac temp1.mp4
ffmpeg -i clip2.avi -c:v libx264 -c:a aac temp2.mp4

# Run standard concatenation map on the fixed temp files
printf "file '%s'\n" temp1.mp4 temp2.mp4 > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

## 💡 Extra: Trimming before merging
If you need to cut out dead air in `clip1.mp4` before sending it to the concat list:
```bash
# Cuts starting at second 10, running until minute 1:30
ffmpeg -ss 00:00:10 -to 00:01:30 -i clip1.mp4 -c copy trimmed_clip1.mp4
```
