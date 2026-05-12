---
tags: ["python", "audio", "whisper", "transcription"]
---
# Transcribe Audio with Whisper (Python)

Transcribes any audio file (MP3, OGG, WAV, M4A, etc.) to text using OpenAI Whisper locally — no API key required.

## Dependencies

```bash
pip install openai-whisper
```

Also requires `ffmpeg` installed on the system:

```bash
# Arch/Manjaro
sudo pacman -S ffmpeg

# Debian/Ubuntu
sudo apt install ffmpeg
```

## Usage

Run the script with the path to your audio file. Supported models: `tiny`, `base`, `small`, `medium`, `large`. Larger models are more accurate but slower.

## Code

```python
import sys
import whisper

AUDIO_FILE = "recording.ogg"   # change to your file
MODEL_SIZE = "base"             # tiny | base | small | medium | large

try:
    model = whisper.load_model(MODEL_SIZE)
except Exception as e:
    sys.exit(f"Failed to load model: {e}")

try:
    result = model.transcribe(AUDIO_FILE)
    print(result["text"])
except Exception as e:
    sys.exit(f"Transcription failed: {e}")
```

## Model size reference

| Model | VRAM | Relative speed |
|-------|------|----------------|
| `tiny` | ~1 GB | Fastest |
| `base` | ~1 GB | Fast |
| `small` | ~2 GB | Balanced |
| `medium` | ~5 GB | Accurate |
| `large` | ~10 GB | Most accurate |
