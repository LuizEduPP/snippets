---
tags: ["python", "images", "sprite", "crop"]
---
# Crop Sprite Sheet — Interactive Grid

Interactive visual tool for defining cut lines on a sprite image and exporting each cell as a separate file. Uses OpenCV to display a scaled preview and track the mouse position in real time.

## Dependencies

```bash
pip install opencv-python
```

## Usage

1. Set `image_path` to your sprite file
2. Run the script
3. In the window that opens:
   - **`H`** — add a horizontal cut line at the current mouse position
   - **`V`** — add a vertical cut line at the current mouse position
   - **`R`** — clear all lines
   - **`Enter`** — crop and save all cells to `./crops/`

Output files follow the pattern: `crops/crop_row_col_timestamp_filename.png`

## Code

```python
import cv2
import os

image_path = "sprite.png"
timestamp = image_path.split(".")[0]
img = cv2.imread(image_path)
clone = img.copy()

DISPLAY_WIDTH = 800
scale = DISPLAY_WIDTH / img.shape[1]
display_height = int(img.shape[0] * scale)
display_img = cv2.resize(clone, (DISPLAY_WIDTH, display_height))

horizontal_lines = []
vertical_lines = []
mouse_x = 0
mouse_y = 0

def mouse_move(event, x, y, flags, param):
    global mouse_x, mouse_y
    if event == cv2.EVENT_MOUSEMOVE:
        mouse_x = x
        mouse_y = y

cv2.namedWindow("Sprite Cutter (H/V to add lines, Enter to crop)")
cv2.setMouseCallback("Sprite Cutter (H/V to add lines, Enter to crop)", mouse_move)

while True:
    preview = display_img.copy()

    for y in horizontal_lines:
        ys = int(y * scale)
        cv2.line(preview, (0, ys), (preview.shape[1], ys), (0, 255, 0), 1)
    for x in vertical_lines:
        xs = int(x * scale)
        cv2.line(preview, (xs, 0), (xs, preview.shape[0]), (255, 0, 0), 1)

    cv2.line(preview, (0, mouse_y), (preview.shape[1], mouse_y), (100, 255, 100), 1)
    cv2.line(preview, (mouse_x, 0), (mouse_x, preview.shape[0]), (100, 255, 100), 1)

    cv2.imshow("Sprite Cutter (H/V to add lines, Enter to crop)", preview)
    key = cv2.waitKey(1) & 0xFF

    if key == ord("h"):
        real = int(mouse_y / scale)
        if real not in horizontal_lines:
            horizontal_lines.append(real)
            horizontal_lines.sort()
    elif key == ord("v"):
        real = int(mouse_x / scale)
        if real not in vertical_lines:
            vertical_lines.append(real)
            vertical_lines.sort()
    elif key == ord("r"):
        horizontal_lines.clear()
        vertical_lines.clear()
    elif key == 13:  # Enter
        if not horizontal_lines or not vertical_lines:
            print("Add at least one horizontal and one vertical line.")
            continue

        os.makedirs("crops", exist_ok=True)

        for i in range(len(horizontal_lines) - 1):
            for j in range(len(vertical_lines) - 1):
                y1 = horizontal_lines[i]
                y2 = horizontal_lines[i + 1]
                x1 = vertical_lines[j]
                x2 = vertical_lines[j + 1]
                crop = clone[y1:y2, x1:x2]
                name = f"crops/crop_{i+1}_{j+1}_{timestamp}_{image_path}"
                cv2.imwrite(name, crop)
                print(f"Saved: {name}")
```
