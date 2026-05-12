---
tags: ["python", "video", "whisper", "transcription", "moviepy"]
---
# Extract Text from Video (Whisper + moviepy)

Extracts the audio track from a video file and transcribes it to text using OpenAI Whisper. Works with MP4, MKV, AVI, and other formats.

## Dependencies

```bash
pip install openai-whisper moviepy
```

## Code

```python
import whisper
import moviepy.editor as mp
import os

def transcribe_video(video_path: str, model_size: str = "base") -> str:
    """
    Extracts audio from a video file and returns the transcription.

    Args:
        video_path: Path to the video file (MP4, MKV, AVI, etc.)
        model_size: Whisper model — "tiny", "base", "small", "medium", "large"

    Returns:
        Transcribed text as a string.
    """
    audio_path = "temp_audio.wav"

    # Extract audio track
    clip = mp.VideoFileClip(video_path)
    clip.audio.write_audiofile(audio_path, codec="pcm_s16le", verbose=False, logger=None)
    clip.close()

    # Transcribe
    model = whisper.load_model(model_size)
    result = model.transcribe(audio_path)

    # Cleanup temp file
    os.remove(audio_path)

    return result["text"]


if __name__ == "__main__":
    text = transcribe_video("video.mp4", model_size="base")
    print(text)

    # Save to file
    with open("transcription.txt", "w", encoding="utf-8") as f:
        f.write(text)
    print("Saved to transcription.txt")
```

---

## Notes

- `"base"` model is a good default; use `"small"` or `"medium"` for better accuracy on technical content.
- The function saves a temporary WAV file during processing — it is deleted automatically.
- For long videos (>30 min), consider chunking the audio with `moviepy` before transcribing.
- Whisper auto-detects the language; force it with `model.transcribe(audio_path, language="pt")`.
