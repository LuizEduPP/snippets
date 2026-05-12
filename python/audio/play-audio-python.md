---
tags: ["python", "audio", "simpleaudio", "pygame"]
---
# Play Audio Files in Python

Plays WAV and MP3 files from Python using `simpleaudio` or `pygame` — replacements for the broken `playsound` library.

## Dependencies

```bash
# Option 1 — simpleaudio (WAV only, lightweight)
pip install simpleaudio

# Option 2 — pygame (WAV + MP3, more features)
pip install pygame
```

## Code

### simpleaudio — WAV playback

```python
import simpleaudio as sa

wave_obj = sa.WaveObject.from_wave_file("sound.wav")
play_obj = wave_obj.play()
play_obj.wait_done()  # blocks until finished
```

### pygame — WAV or MP3 playback

```python
import pygame

pygame.mixer.init()
pygame.mixer.music.load("sound.mp3")  # or .wav
pygame.mixer.music.play()

# Wait for playback to finish
while pygame.mixer.music.get_busy():
    pass
```

### pygame — play multiple sounds simultaneously

```python
import pygame

pygame.mixer.init()
pygame.mixer.set_num_channels(8)

sound1 = pygame.mixer.Sound("click.wav")
sound2 = pygame.mixer.Sound("beep.wav")

sound1.play()
sound2.play()
pygame.time.wait(2000)
```

---

## Comparison

| Library | WAV | MP3 | Blocking | Notes |
|---------|-----|-----|----------|-------|
| `simpleaudio` | ✅ | ❌ | optional | Lightweight, no dependencies |
| `pygame.mixer` | ✅ | ✅ | manual | Full-featured, requires display-less init |
| `pydub` | ✅ | ✅ | yes | Requires `ffmpeg` installed |
