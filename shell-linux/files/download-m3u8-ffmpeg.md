---
tags: ["shell-linux", "files", "ffmpeg", "m3u8", "hls", "download"]
---
# Download m3u8 Stream with FFmpeg

Downloads an HLS (m3u8) stream and saves it as a single MP4 file using FFmpeg. Works with live streams and VOD playlists.

Paste and run directly in the terminal — no file needed.

## Command

### Download and remux (fastest — no re-encoding)

```bash
ffmpeg -i "https://example.com/playlist.m3u8" \
  -c copy \
  -bsf:a aac_adtstoasc \
  output.mp4
```

> `-c copy` remuxes the stream without re-encoding. `-bsf:a aac_adtstoasc` converts the AAC audio bitstream format to be compatible with MP4 containers.

### If the stream fails at the start (live index issue)

```bash
ffmpeg -live_start_index 0 \
  -i "https://example.com/playlist.m3u8" \
  -c copy \
  -bsf:a aac_adtstoasc \
  output.mp4
```

> `-live_start_index 0` forces FFmpeg to start from the first available segment instead of the live edge, which prevents index-related failures.

### Local playlist file

```bash
ffmpeg -i playlist.m3u8 -c copy -bsf:a aac_adtstoasc output.mp4
```
