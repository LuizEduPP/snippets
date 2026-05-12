---
tags: ["python", "media", "audio", "whisper", "transcription", "automation"]
---
# Transcribe Audio using Whisper (Python)

A fully operational Python framework to ingest any audio format (`.MP3`, `.OGG`, `.WAV`, `.M4A`, etc.) and automatically spit out highly accurate text transcripts using OpenAI's offline Whisper model. zero cloud API keys or subscriptions required.

## 🛠️ How it works under the hood

1. **`ffmpeg`**: Whisper cannot read standard compressed formats. Before feeding data to its neural network, the Whisper package secretly shells out to your system's `ffmpeg` to decompress the audio stream directly into standard 16KHz floats.
2. **`whisper.load_model()`**: Allocates memory on your GPU (if CUDA is enabled) or CPU/RAM and loads the chosen neural matrices. 3. **`model.transcribe()`**: Scans through the tensor window arrays analyzing linguistic shifts probabilistically, returning a mapped `.json` variant containing the translation tree.

---

## ⚡ Setup / Installation

1. **Install Python Binding**:
```bash
pip install openai-whisper
```

2. **Ensure FFmpeg binary exists**:
```bash
# Ubuntu / Debian
sudo apt install ffmpeg

# Arch Linux / Manjaro
sudo pacman -S ffmpeg
```

---

## 🚀 Usage Guide

Replace `recording.ogg` with the explicit path to the audio file you wish to target. 

Save it as `transcriber.py` and run it:

```python
import sys
import whisper

AUDIO_FILE = "recording.ogg" 
MODEL_SIZE = "base" # Options: tiny | base | small | medium | large

# Safely preload the model framework and handle out-of-memory errors
try:
 print(f"Loading '{MODEL_SIZE}' AI model...")
 model = whisper.load_model(MODEL_SIZE)
except Exception as e:
 sys.exit(f"Failed to load model: {e}")

# Push the audio through the processor safely
try:
 print(f"Transcribing '{AUDIO_FILE}'...")
 result = model.transcribe(AUDIO_FILE)
 
 print("\n📝 Output Translation:\n")
 print(result["text"])
 
except Exception as e:
 sys.exit(f"Transcription failed: {e}")
```

## 📊 Model Size Reference

Depending on the system compiling it, use the baseline metric guide below to pick your `MODEL_SIZE` constraint correctly avoiding crashing:

| Model | Estimated System VRAM | Run Speed | Best For |
|-------|------|----------------|----------|
| `tiny` | ~1 GB | Blistering | Short basic sentence confirmation |
| `base` | ~1 GB | Fast | **Recommended universal default** |
| `small` | ~2 GB | Moderate | Longer podcasts w/ minimal jargon |
| `medium` | ~5 GB | Slow | Medical, Code, and heavy syntax translation |
| `large` | ~10 GB | Extremely Slow | Professional archiving/subtitle burning |
