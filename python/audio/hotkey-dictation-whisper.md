---
tags: ["python", "audio", "whisper", "hotkey", "pyqt5"]
---
# Hotkey Speech Dictation (Whisper + pynput)

Records audio on a global keyboard shortcut and transcribes it using Whisper. Runs silently in the system tray (PyQt5).

## Dependencies

```bash
pip install openai-whisper pynput sounddevice numpy PyQt5
sudo apt install sox libnotify-bin    # Debian/Ubuntu
```

## Code

### Minimal — record on hotkey press and print transcription

```python
import whisper
import pynput
from pynput import keyboard
import sounddevice as sd
import numpy as np

model = whisper.load_model("base")  # options: tiny, base, small, medium, large

HOTKEY = {keyboard.Key.alt, keyboard.Key.shift, keyboard.KeyCode.from_char("d")}
pressed = set()

def record_and_transcribe():
    duration = 5       # seconds to record
    sample_rate = 16000
    print("Recording...")
    audio = sd.rec(
        int(duration * sample_rate),
        samplerate=sample_rate,
        channels=1,
        dtype="float32"
    )
    sd.wait()
    result = model.transcribe(audio.flatten())
    print(result["text"])

def on_press(key):
    if key in HOTKEY:
        pressed.add(key)
        if HOTKEY.issubset(pressed):
            record_and_transcribe()

def on_release(key):
    pressed.discard(key)

with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    print("Listening... Press Alt+Shift+D to dictate.")
    listener.join()
```

---

### System tray launcher (PyQt5)

```python
import sys
import subprocess
from PyQt5.QtWidgets import QApplication, QSystemTrayIcon, QMenu
from PyQt5.QtGui import QIcon

class DictationTray(QSystemTrayIcon):
    def __init__(self):
        super().__init__()
        self.setIcon(QIcon.fromTheme("audio-input-microphone"))
        menu = QMenu()
        menu.addAction("Start Dictation", self.start)
        menu.addAction("Quit", QApplication.quit)
        self.setContextMenu(menu)

    def start(self):
        subprocess.Popen(["python3", "dictation.py"])

app = QApplication(sys.argv)
tray = DictationTray()
tray.show()
sys.exit(app.exec_())
```

---

## Notes

- `"tiny"` model is fastest; `"base"` is a good balance of speed and accuracy.
- Whisper auto-detects the language. Force a language with `model.transcribe(audio, language="en")`.
- For long recordings, chunk the audio or use `"small"` / `"medium"` models.
