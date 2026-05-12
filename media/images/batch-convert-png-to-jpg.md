---
tags: ["python", "media", "images", "png", "jpg", "convert", "automation"]
---
# Batch Convert PNG images to JPG (Python)

A pure Python script to convert thousands of `.png` files inside a directory to standard `.jpg` formats. It handles creation of output folders automatically and solves the dreaded Alpha transparency channel crash universally.

## 🛠️ How it works under the hood

1. **`Pillow / PIL`**: The Python Imaging Library fork. It handles reading/writing binary image buffers. 2. **`os.makedirs(..., exist_ok=True)`**: Safely creates the target destination directory if it doesn't already exist, skipping the crash error if it does.
3. **`img.convert("RGB")`**: The core magic. `.png` files almost strictly retain RGBA profiles (Red, Green, Blue, Alpha/Transparency). The JPEG standard strictly does not support Alpha data. If you bypass `.convert("RGB")` prior to saving, Pillow will crash intentionally (`cannot write mode RGBA as JPEG` error).

---

## ⚡ Setup / Installation

Install Pillow :

```bash
pip install Pillow
```

---

## 🚀 Usage Guide

Save the script. Ensure your target unmapped `.png` files are sitting inside the `INPUT_FOLDER`. 

```python
from PIL import Image
import os

INPUT_FOLDER = "images_png"
OUTPUT_FOLDER = "images_jpg"

# Automatically spawn the target dumping ground folder os.makedirs(OUTPUT_FOLDER, exist_ok=True)

converted = 0

# Loop all items logically in the input baseline
for filename in os.listdir(INPUT_FOLDER):
 
 # Filter for matching files
 if filename.lower().endswith(".png"):
 src = os.path.join(INPUT_FOLDER, filename)
 
 # Strip the old `.png` extension completely replacing it with `.jpg` internally
 dst = os.path.join(OUTPUT_FOLDER, os.path.splitext(filename)[0] + ".jpg")

 # Context manager safely opens, translates the channel space, and re-closes
 with Image.open(src) as img:
 img.convert("RGB").save(dst, "JPEG")
 
 converted += 1

print(f"✅ Success: {converted} file(s) safely converted and bundled into {OUTPUT_FOLDER}/")
```
