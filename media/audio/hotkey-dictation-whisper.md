---
tags: ["python", "media", "audio", "whisper", "hotkey", "automation"]
---
# Hotkey Speech Dictation (Whisper + pynput)

This script creates a native dictation tool. It binds to a global keyboard shortcut (like Alt+Shift+D), records your voice from your microphone, and translates it entirely offline using OpenAI's Whisper model. Optionally, it can reside in your system tray without popping up ugly terminal windows.

## 🛠️ How it works under the hood

1. **`pynput`**: Safely binds deeply into the OS's keyboard event listeners to intercept specific key combinations universally (no matter what window you are focused on).
2. **`sounddevice`**: Bypasses heavy multimedia packages to directly interface with your hardware's audio input. It buffers the waveform into numpy arrays.
3. **`whisper.load_model()`**: Preloads the AI model directly into memory so it activates instantly upon pressing your designated hotkeys.
4. **`audio.flatten()`**: The audio stream comes in as a 2D matrix (shape: `seconds * sample_rate`, `1 channel`). Whisper's neural engine assumes a flattened 1-dimensional array, so flattening ensures the ingestion is perfect.

---

## ⚡ Setup / Installation

Install the underlying stream captures and neural arrays :

```bash
pip install openai-whisper pynput sounddevice numpy PyQt5

# If you are on Linux, ensure audio stream handling is installed system-wide:
sudo apt install sox libnotify-bin
```

---

## 🚀 Usage Guide

### 1. Minimal Version (Terminal execution)
Save this as `dictation.py`. Pressing `Alt+Shift+D` will instantly record 5 seconds of audio and output the text directly.

```python
import whisper
from pynput import keyboard
import sounddevice as sd
import numpy as np

# Load neural weights
model = whisper.load_model("base")

# Define the global shortcut
HOTKEY = {keyboard.Key.alt, keyboard.Key.shift, keyboard.KeyCode.from_char("d")}
pressed = set()

def record_and_transcribe():
 duration = 5 # Amount of time to record once triggered
 sample_rate = 16000
 print("🎙️ Recording...")
 
 # Grab the hardware device audio = sd.rec(
 int(duration * sample_rate),
 samplerate=sample_rate,
 channels=1,
 dtype="float32"
 )
 sd.wait() # Block until duration is complete
 
 # Send flattened array to AI
 result = model.transcribe(audio.flatten())
 print("\n📝 Output:", result["text"])

def on_press(key):
 if key in HOTKEY:
 pressed.add(key)
 if HOTKEY.issubset(pressed):
 record_and_transcribe()

def on_release(key):
 pressed.discard(key)

# The listener runs globally in the background
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
 print("🟢 Listening... Press Alt+Shift+D to dictate.")
 listener.join()
```

### 2. System Tray Launcher (PyQt5)
If you want to boot the above script silently on startup and nestle it in your taskbar, use this wrapper block. Save it as `tray.py`.

```python
import sys
import subprocess
from PyQt5.QtWidgets import QApplication, QSystemTrayIcon, QMenu
from PyQt5.QtGui import QIcon

class DictationTray(QSystemTrayIcon):
 def __init__(self):
 super().__init__()
 self.setIcon(QIcon.fromTheme("audio-input-microphone"))
 
 # Build right-click context
 menu = QMenu()
 menu.addAction("Start Dictation Background", self.start)
 menu.addAction("Quit", QApplication.quit)
 self.setContextMenu(menu)

 def start(self):
 # Spawns the dictation script completely detached from UI
 subprocess.Popen(["python3", "dictation.py"])

app = QApplication(sys.argv)
tray = DictationTray()
tray.show()
sys.exit(app.exec_())
```

## 🐛 Troubleshooting & Tips
- The `"tiny"` model grabs incredibly fast results, but hallucinates heavily. Stay on `"base"`.
- Want continuous dictation instead of fixed 5-second blocks? You would have to modify `sounddevice.rec` to use an `InputStream` callback loop.
