---
tags: ["linux", "media", "ffmpeg", "m3u8", "download"]
---
# Download an HLS (m3u8) Stream with FFmpeg

This command directly intercepts streaming video manifests (`.m3u8` playlists) used by platforms like Twitch or online TV systems, and translates the segments into a standard, playable `.mp4` file. It works on both Live streams and Video On Demand (VOD) archives.

## 🛠️ How it works under the hood

1. **`ffmpeg`**: The Swiss Army knife for audio/video stream manipulation in Linux.
2. **`-i "..."`**: Passes the `.m3u8` playlist URL to the input parser.
3. **`-c copy`**: Tells ffmpeg to cleanly copy the video chunks *without re-encoding them*. Re-encoding would require immense CPU power and reduce video quality. "Copying" is nearly instantaneous.
4. **`-bsf:a aac_adtstoasc`**: A specific Bitstream Filter formatting rule. `m3u8` streams usually transmit audio in the `ADTS` container type. This filter safely repackages the stream into the `.MP4` container standard without losing quality.
5. **`output.mp4`**: The name of the final file you are generating.

---

## 🚀 Usage Guide

Ensure you have `ffmpeg` installed (e.g. `sudo apt install ffmpeg`). Then paste this into your terminal:

### 1. Fast Direct Download (Remuxing)
This is the fastest method, as it simply copies streams bit-by-bit. Grab the `.m3u8` URL from your browser's Network Developer Tools.

```bash
ffmpeg -i "https://example.com/playlist.m3u8" \
 -c copy \
 -bsf:a aac_adtstoasc \
 output.mp4
```

### 2. Live Stream Edge Fixes
Sometimes, `ffmpeg` fails immediately upon connecting to a stream, spewing index or timing errors (because the playlist is shifting). This flag forces `ffmpeg` to capture chunks starting exactly from index zero of the active buffer block.

```bash
ffmpeg -live_start_index 0 \
 -i "https://example.com/playlist.m3u8" \
 -c copy \
 -bsf:a aac_adtstoasc \
 output.mp4
```

### 3. Local Offline Playlists
If you already downloaded the `.m3u8` text file locally and merely want to stitch the video using it as a map:

```bash
ffmpeg -i local_playlist.m3u8 -c copy -bsf:a aac_adtstoasc output.mp4
```
