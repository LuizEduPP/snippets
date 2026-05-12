---
tags: ["python", "media", "audio", "simpleaudio", "pygame", "playback"]
---
# Play Audio Files in Python

A reliable guide to playing `.WAV` and `.MP3` files directly from execution scripts using either `simpleaudio` or `pygame`. This entirely bypasses the traditionally recommended but fundamentally broken `playsound` library.

## 🛠️ How it works under the hood

1. **`simpleaudio`**: A minimalist C-extension wrapper. It reads raw PCM data from a WAV byte buffer and fires it straight to the OS ALSA/CoreAudio backend. No background processing, extremely lightweight.
2. **`pygame.mixer`**: A fully-fledged SDL abstraction layer. It initializes a virtual audio canvas (the mixer), buffers `.mp3` decoding live, and runs it on non-blocking background threads — allowing you to manage multi-channel simultaneous sounds.

---

## ⚡ Setup / Installation

Depending on your use case, install your handler:

```bash
# Option 1: Lightweight WAV playback only
pip install simpleaudio

# Option 2: Full-featured WAV/MP3 simultaneous playback
pip install pygame
```

---

## 🚀 Usage Guide

### 1. Minimal `simpleaudio` method (WAV Only)
The absolute fastest way to drop a sound effect in a script. It will block the Python thread until the sound finishes playing.

```python
import simpleaudio as sa

wave_obj = sa.WaveObject.from_wave_file("sound.wav")
play_obj = wave_obj.play()

# Block script execution until complete
play_obj.wait_done() 
```

### 2. Full `pygame` method (WAV & MP3)
Pygame plays sounds asynchronously (in the background). Because it doesn't pause the script, we have to deliberately tell Python to wait `while` it plays, or else the script will terminate instantly, ending the sound track.

```python
import pygame

# Initialize the SDL Mixer layer
pygame.mixer.init()

# Buffer the mp3 array into memory
pygame.mixer.music.load("sound.mp3")
pygame.mixer.music.play()

# Keep script alive while the background thread plays
while pygame.mixer.music.get_busy():
 pass
```

### 3. Pygame Simultaneous Tracks (Multi-Channel)
If you want to play UI interface clicks and background music simultaneously on different threads:

```python
import pygame

pygame.mixer.init()
pygame.mixer.set_num_channels(8) # Create 8 isolated sound threads

sound1 = pygame.mixer.Sound("click.wav")
sound2 = pygame.mixer.Sound("beep.wav")

# Both trigger simultaneously alongside each other
sound1.play()
sound2.play()

# Wait 2000 milliseconds for them to finish before ending the script
pygame.time.wait(2000)
```

## 📊 Evaluation Matrix

| Library | WAV | MP3 | Blocking | Notes |
|---------|-----|-----|----------|-------|
| `simpleaudio` | ✅ | ❌ | optional | Lightweight, zero external dependencies |
| `pygame.mixer` | ✅ | ✅ | manual | Heavy feature-set, requires display-less SDL init |
| `pydub` | ✅ | ✅ | yes | *(Not covered here, but requires massive ffmpeg binary)* |
