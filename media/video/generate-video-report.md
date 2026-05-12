---
tags: ["python", "video", "report", "whisper", "ocr", "tesseract", "moviepy"]
---
# Generate Video Report (Whisper + OCR)

Takes a video file and produces a self-contained HTML report. Each section of the report shows the spoken words (transcribed by Whisper) and the visible text on screen (extracted by Tesseract OCR), paired with a captured frame from that moment.

## 🛠️ How it works under the hood

1. **`moviepy`**: Reads the video container and extracts its audio stream into a temporary `.wav` file on disk, which Whisper requires as input.
2. **`whisper`**: Loads a local model (no internet needed) and processes the `.wav` file into timed text segments. Each segment contains a `start` timestamp and the transcribed sentence.
3. **`cv2.VideoCapture`**: Opens the video file and seeks to specific frame positions by computing `second × fps`. For every sampled second, it saves the raw JPEG and also encodes it as a base64 string for embedding directly inside the HTML.
4. **`pytesseract.image_to_string`**: Converts each frame to grayscale before passing it to Tesseract. Grayscale improves OCR accuracy on text-heavy screens. The `lang="por"` parameter sets the recognition language to Portuguese.
5. **`jinja2.Template`**: Takes the list of blocks (timestamp, speech, screen text, base64 image) and renders them into styled HTML cards, producing a single portable `.html` file with no external dependencies.

---

## 🚀 Usage Guide

### 1. Install system dependencies
```bash
# Ubuntu/Debian
sudo apt install tesseract-ocr tesseract-ocr-por
```

### 2. Install Python packages
```bash
pip install opencv-python openai-whisper moviepy pytesseract tqdm jinja2
```

### 3. Run the script
```python
import os
import cv2
import whisper
import base64
import moviepy.editor as mp
from tqdm import tqdm
from jinja2 import Template
from pathlib import Path

try:
    import pytesseract
except ImportError:
    print("pytesseract not installed. Run: pip install pytesseract")
    exit(1)

VIDEO_PATH = input("Enter video path (e.g. /path/to/video.mp4): ").strip()
if not Path(VIDEO_PATH).exists():
    print("Video file not found.")
    exit(1)

FRAME_INTERVAL = 3   # Sample one frame every N seconds
WHISPER_MODEL = "base"

def format_time(s):
    t = int(s)
    return {
        "slug": f"{t//3600:02d}_{(t%3600)//60:02d}_{t%60:02d}",
        "label": f"{t//3600:02d}:{(t%3600)//60:02d}:{t%60:02d}"
    }

def to_seconds(hms):
    h, m, s = map(int, hms.split(":"))
    return h * 3600 + m * 60 + s

def extract_audio(video_path, audio_path):
    print("Extracting audio...")
    clip = mp.VideoFileClip(video_path)
    clip.audio.write_audiofile(audio_path, codec='pcm_s16le')

def transcribe(audio_path):
    print("Transcribing with Whisper...")
    model = whisper.load_model(WHISPER_MODEL)
    result = model.transcribe(audio_path, verbose=True, language="pt", task="transcribe")
    if not result.get('segments'):
        print("Warning: no audio segments found.")
        return []
    return result['segments']

def extract_frames_and_ocr(video_path, interval, output_dir):
    print("Extracting frames and running OCR...")
    cap = cv2.VideoCapture(video_path)
    fps = cap.get(cv2.CAP_PROP_FPS)
    duration = int(cap.get(cv2.CAP_PROP_FRAME_COUNT) / fps)
    results = []

    for s in tqdm(range(0, duration, interval)):
        cap.set(cv2.CAP_PROP_POS_FRAMES, int(s * fps))
        ret, frame = cap.read()
        if not ret:
            continue

        time = format_time(s)
        cv2.imwrite(os.path.join(output_dir, f"frame_{time['slug']}.jpg"), frame)

        ok, buf = cv2.imencode('.jpg', frame)
        img_b64 = f"data:image/jpeg;base64,{base64.b64encode(buf).decode()}" if ok else None

        try:
            gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
            text = pytesseract.image_to_string(
                cv2.resize(gray, (1280, 720)), lang="por", timeout=10
            ).strip()
        except Exception as e:
            text = f"[OCR error: {e}]"

        results.append({"time": time['label'], "slug": time['slug'], "image": img_b64, "text": text})

    cap.release()
    return results

HTML = """<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Video Report</title>
<style>
body { font-family: sans-serif; margin: 2em; background: #f0f0f0; }
.card { background: #fff; padding: 1em; margin-bottom: 1.5em; border-radius: 8px;
        box-shadow: 0 2px 6px rgba(0,0,0,0.1); }
img { max-width: 100%; border-radius: 5px; margin-top: 0.5em; }
h2 { margin: 0 0 0.3em; }
</style>
</head>
<body>
<h1>Video Report</h1>
{% for b in blocks %}
<div class="card" id="t{{ b.slug }}">
  <h2>{{ b.time }}</h2>
  <p><strong>Speech:</strong> {{ b.speech }}</p>
  {% if b.screen_text %}<p><strong>Screen text:</strong> {{ b.screen_text }}</p>{% endif %}
  {% if b.image %}<img src="{{ b.image }}" alt="Frame {{ b.time }}">{% endif %}
</div>
{% endfor %}
</body>
</html>"""

def generate_html(transcriptions, frames, output_dir):
    print("Generating HTML report...")
    frames_by_time = {to_seconds(f['time']): f for f in frames}
    sorted_times = sorted(frames_by_time)
    blocks = []

    if not transcriptions and frames:
        for f in frames:
            blocks.append({"time": f['time'], "slug": f['slug'],
                           "speech": "No transcription", "image": f["image"], "screen_text": f["text"]})
    else:
        for seg in transcriptions:
            if 'start' not in seg or 'text' not in seg:
                continue
            s = int(seg['start'])
            t = format_time(s)
            closest = frames_by_time.get(min(sorted_times, key=lambda x: abs(x - s)))
            blocks.append({
                "time": t['label'], "slug": t['slug'],
                "speech": seg['text'].strip(),
                "image": closest["image"] if closest else None,
                "screen_text": closest["text"] if closest and closest["text"] else None
            })

    if not blocks:
        blocks = [{"time": "00:00:00", "slug": "00_00_00",
                   "speech": "No transcription available.", "image": None, "screen_text": None}]

    out = os.path.join(output_dir, "report.html")
    with open(out, "w", encoding="utf-8") as f:
        f.write(Template(HTML).render(blocks=blocks))
    print(f"Report saved: {out} ({len(blocks)} segments)")

def main():
    if Path(VIDEO_PATH).suffix.lower() not in ['.mp4', '.avi', '.mkv', '.mov', '.wmv']:
        print(f"Unsupported format: {Path(VIDEO_PATH).suffix}")
        return

    name = Path(VIDEO_PATH).stem
    out_dir = os.path.join("output", name)
    os.makedirs(out_dir, exist_ok=True)
    audio = os.path.join(out_dir, "audio.wav")

    extract_audio(VIDEO_PATH, audio)
    segments = transcribe(audio)
    frames = extract_frames_and_ocr(VIDEO_PATH, FRAME_INTERVAL, out_dir)
    generate_html(segments, frames, out_dir)
    os.remove(audio)

if __name__ == "__main__":
    main()
```
