---
tags: ["python", "dev-tools", "gcode", "automation", "3d-printing"]
---
# G-Code Post-Processing Runner

A modular master script that chains multiple Python post-processing algorithms consecutively onto raw G-Code right after standard slicing applications (like PrusaSlicer, SuperSlicer, or Cura) dump the file. Each configured algorithm parses and overrides output strings cascading sequentially down the stack.

## 🛠️ How it works under the hood

1. **`add_temperature_commands()`**: Unconditionally intercepts the unheated initial G-Code array and dynamically writes strict target values (`M190` Bed / `M109` Nozzle) preventing cold hardware extrusions outright.
2. **`subprocess.check_call()`**: Instead of executing all algorithms locally in standard memory, the runner spawns completely sterile external `python3` instances parsing independent `.py` script logic arrays to avoid internal cross-contamination.
3. **`current_input` Pipeline Shift**: Upon each block's completion, the old output becomes the absolute new base layer input dynamically through `os.path.splitext()` shifting.

---

## ⚡ Setup / Installation

Since it relies purely on vanilla Python standard utilities (`os`, `subprocess`, `logging`), there are NO third-party requirements or dependencies.

Attach the script physically to the Slicer application configurations:
* **PrusaSlicer**: Print Settings → Output options → Post-processing scripts → `/usr/bin/python3 /path/to/post_process_master.py;`

---

## 🚀 Usage Guide

```python
import os
import sys
import subprocess
import logging
import traceback

# --- Configuration ---
SCRIPTS_DIR = "/home/user/code/prusa/scripts"
LOG_FILE = "/home/user/code/prusa/post_process_master.log"

# Define the absolute sequential execution cascading structure layer by layer.
PIPELINE = [
 "anti_elephant_foot.py",
 "limit_retractions.py",
 "optimised_timelapse.py",
]

# --- Logging setup ---
logging.basicConfig(
 filename=LOG_FILE,
 filemode="a",
 format="%(asctime)s - %(levelname)s - %(message)s",
 level=logging.INFO,
)
logger = logging.getLogger()

def add_temperature_commands(gcode_file: str) -> None:
 """Prepend raw bed and nozzle safe wait commands structurally to the top slice space."""
 temp_commands = [
 "M190 S65; Wait for bed fully uniform 65°C\n",
 "M109 S210; Wait for nozzle fully uniform 210°C\n",
 ]
 with open(gcode_file, "r") as f:
 lines = f.readlines()
 
 with open(gcode_file, "w") as f:
 f.writelines(temp_commands + lines)
 logger.info("Temperature block parameters appended. ")

def run_script(script_name: str, input_file: str, output_file: str) -> None:
 """Instantiate a sterile independent Python execution process layer for pipeline traversal."""
 script_path = os.path.join(SCRIPTS_DIR, script_name)
 cmd = ["python3", script_path, input_file, output_file]
 
 logger.info(f"Running pipeline segment: {' '.join(cmd)}")
 subprocess.check_call(cmd)
 logger.info(f"Segment [ {script_name} ] completed.")

def main(gcode_file: str) -> None:
 try:
 # Phase 1: Override Temperatures
 add_temperature_commands(gcode_file)

 # Phase 2: Traverse Pipeline stack pushing the file to downstream layers
 current_input = gcode_file
 
 for script in PIPELINE:
 base, ext = os.path.splitext(gcode_file)
 output = f"{base}_{script.replace('.py', '')}{ext}"
 
 run_script(script, current_input, output)
 
 # Elevate output to become new base input
 current_input = output

 logger.info("✅ All post-processing G-Code stack actions finished without faults.")

 except Exception as e:
 logger.error(f"❌ Pipeline logic stack drastically failed: {e}")
 traceback.print_exc()

if __name__ == "__main__":
 if len(sys.argv) < 2:
 print("Usage: python3 post_process_master.py <target_payload.gcode>")
 sys.exit(1)
 main(sys.argv[1])
```
