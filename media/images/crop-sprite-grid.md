---
tags: ["python", "media", "images", "sprite", "crop", "automation"]
---
# Crop Sprite Sheet (Interactive Grid Editor)

A robust visual script running on top of OpenCV that automatically maps out a giant image file (like a massive 2D game sprite sheet) and lets the user actively slice the image using physical horizontal and vertical cutlines. Once defined through the UI, the script intelligently maps out the resulting bounding boxes and slices out every cell uniquely into an output file. 

## 🛠️ How it works under the hood

1. **`cv2 (OpenCV)`**: An extremely low-level computer vision library capable of intercepting live mouse streams and painting matrix pixels. 2. **Key Listeners (`cv2.waitKey()`)**: Actively polls the user's keystrokes. Pressing `H` paints a horizontal cross section, generating mathematical coordinate borders.
3. **Bounding Slices**: The mathematical array manipulation `img[y1:y2, x1:x2]` takes the mapped grid boundaries drawn by the user and directly isolates standard Numpy subarrays out of the core image without external memory hits. 

---

## ⚡ Setup / Installation

Install the compiled computer vision array mapping logic :

```bash
pip install opencv-python
```

---

## 🚀 Usage Guide

Save the following block to `slicer.py` and run it against a valid sprite image.

### User Interface Controls
Once the window spawns, position your mouse on the exact cutting boundary edge you wish to segment, and press:
- **`H`** — Set a persistent Horizontal cut line.
- **`V`** — Set a persistent Vertical cut line.
- **`R`** — Reset/Clear all drawn lines.
- **`Enter`** — Slices the image against all painted coordinate lines and exports every isolated box immediately into `./crops/`.

### Source Code

```python
import cv2
import os
from datetime import datetime

IMAGE_PATH = "sprite.png"

# Setup visual intercept logic
img = cv2.imread(IMAGE_PATH)
if img is None:
 raise FileNotFoundError(f"Could not load image: {IMAGE_PATH}")

h_lines = []
v_lines = []

def mouse_callback(event, x, y, flags, param):
 """
 Hook to capture the user's live mouse crosshairs actively.
 We merely store the physical coordinates passively for rendering.
 """
 global mouse_x, mouse_y
 if event == cv2.EVENT_MOUSEMOVE:
 mouse_x, mouse_y = x, y

cv2.namedWindow('Sprite Slicer')
cv2.setMouseCallback('Sprite Slicer', mouse_callback)

mouse_x, mouse_y = 0, 0

print("Controls: H=Horizontal line, V=Vertical line, R=Reset, ENTER=Process")

# Open continuous render window native intercept loop
while True:
 render = img.copy()

 # Re-draw the locked lines for y in h_lines:
 cv2.line(render, (0, y), (render.shape[1], y), (0, 255, 0), 1)
 for x in v_lines:
 cv2.line(render, (x, 0), (x, render.shape[0]), (0, 255, 0), 1)

 # Draw the floating guideline dynamically following mouse
 cv2.line(render, (0, mouse_y), (render.shape[1], mouse_y), (200, 200, 200), 1)
 cv2.line(render, (mouse_x, 0), (mouse_x, render.shape[0]), (200, 200, 200), 1)

 cv2.imshow('Sprite Slicer', render)
 key = cv2.waitKey(1) & 0xFF

 if key == ord('h'):
 h_lines.append(mouse_y)
 elif key == ord('v'):
 v_lines.append(mouse_x)
 elif key == ord('r'):
 h_lines.clear()
 v_lines.clear()
 
 # Process slices
 elif key == 13: # ASCII Enter Key
 os.makedirs("crops", exist_ok=True)
 h_bounds = [0] + sorted(h_lines) + [img.shape[0]]
 v_bounds = [0] + sorted(v_lines) + [img.shape[1]]
 
 timestamp = datetime.now().strftime("%H%M%S")
 count = 0
 
 # Sequentially array slice intersections for row in range(len(h_bounds)-1):
 for col in range(len(v_bounds)-1):
 y1, y2 = h_bounds[row], h_bounds[row+1]
 x1, x2 = v_bounds[col], v_bounds[col+1]
 
 # Numpy Slice Matrix
 cell = img[y1:y2, x1:x2]
 
 # Filter empty blocks if cell.shape[0] > 0 and cell.shape[1] > 0:
 out = f"crops/cell_{row}_{col}_{timestamp}.png"
 cv2.imwrite(out, cell)
 count += 1
 
 print(f"✅ Extracted {count} sliced images. ")
 break
 
 # Escape condition elif key == 27:
 break

cv2.destroyAllWindows()
```
