---
tags: ["python", "media", "video", "whisper", "transcription", "automation"]
---
# Extract and Transcribe Text from Video (Whisper + moviepy)

This script isolates the audio pipeline from a bulky video file (like MP4 or MKV) and feeds it directly into OpenAI's native (and completely free/offline) **Whisper AI** model to generate a pristine text transcription.

It handles all intermediate cleanups locally without requiring any cloud API key or telemetry.

## 🛠️ How it works under the hood

1. **`moviepy`**: Used mathematically to decouple the multiplexed video mapping and extract the `pcm_s16le` standard `.WAV` format silently in the background. It is highly robust across standard OS architectures. 
2. **`whisper.load_model()`**: Caches the neural weights into RAM directly. 
 - Uses parameters like `"tiny"`, `"base"`, `"small"`, or `"medium"`. A `"base"` model runs well on nearly all machines, but `"medium"` should be used for critical context outputs (medical/code discussions).
3. **`os.remove(audio_path)`**: Instantly throws out the heavy temporary `.WAV` file once Whisper is done scanning it to keep your hard drive clean.

---

## ⚡ Setup / Installation

Install the required packages via pip:

```bash
pip install openai-whisper moviepy
```
*(Also verify you have standard `ffmpeg` installed on your machine).*

## 🚀 Usage Guide

Save this script as `transcribe.py` and run it via `python3 transcribe.py`. 

```python
import whisper
import moviepy.editor as mp
import os

def transcribe_video(video_path: str, model_size: str = "base") -> str:
 """
 Extracts audio from a video file and returns the transcription. Args:
 video_path: Path to the video file (e.g. "My_Movie.mp4")
 model_size: Whisper model size — "tiny", "base", "small", "medium", "large"

 Returns:
 The extracted AI-translated text string.
 """
 audio_path = "temp_audio.wav"

 # Step 1: Strip the audio timeline silently
 print("🎬 Extracting Audio stream...")
 clip = mp.VideoFileClip(video_path)
 clip.audio.write_audiofile(audio_path, codec="pcm_s16le", verbose=False, logger=None)
 clip.close()

 # Step 2: Inject the audio into the neural model
 print(f"👂 Transcribing with Whisper [{model_size}] model. Please wait...")
 model = whisper.load_model(model_size)
 
 # Optional: Force a specific language flag here if it gets confused # result = model.transcribe(audio_path, language="pt") 
 result = model.transcribe(audio_path)

 # Step 3: Trash the huge temp wav file
 print("🧹 Trashing temporary storage blocks...")
 os.remove(audio_path)

 return result["text"]


# Example Execution Wrapper
if __name__ == "__main__":
 text = transcribe_video("video.mp4", model_size="base")
 print("\n--- Output ---")
 print(text)

 # Automatically save it into a readable text document
 with open("transcription.txt", "w", encoding="utf-8") as f:
 f.write(text)
 print("\n✅ Successfully saved to transcription.txt")
```

## 🐛 Troubleshooting & Tips
- **Massive RAM Usage:** If you try running `"large"` or `"medium"` without a dedicated graphics card (CUDA), your computer may stall. Drop the parameter down to `"base"` to fix it.
- **Huge files over 30 mins:** Whisper can hallucinate if fed an extremely long single audio file. You should chunk the `clip.audio` via `moviepy` before dropping it into `transcribe` if necessary.
