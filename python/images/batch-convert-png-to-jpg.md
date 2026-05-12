---
tags: ["python", "images", "png", "jpg", "convert"]
---
# Batch Convert PNG to JPG (Python)

Converts every `.png` file in a folder to `.jpg` using Pillow. Handles transparency by converting to RGB before saving.

## Dependencies

```bash
pip install Pillow
```

## Usage

Set `INPUT_FOLDER` and `OUTPUT_FOLDER`, then run. The output directory is created automatically if it doesn't exist.

## Code

```python
from PIL import Image
import os

INPUT_FOLDER  = "images_png"
OUTPUT_FOLDER = "images_jpg"

os.makedirs(OUTPUT_FOLDER, exist_ok=True)

converted = 0
for filename in os.listdir(INPUT_FOLDER):
    if filename.lower().endswith(".png"):
        src = os.path.join(INPUT_FOLDER, filename)
        dst = os.path.join(OUTPUT_FOLDER, os.path.splitext(filename)[0] + ".jpg")

        with Image.open(src) as img:
            img.convert("RGB").save(dst, "JPEG")
        converted += 1

print(f"Done: {converted} file(s) converted to {OUTPUT_FOLDER}/")
```

> `.convert("RGB")` is required because PNG supports an alpha channel (RGBA) which JPEG does not. Skipping it raises a `cannot write mode RGBA as JPEG` error.
