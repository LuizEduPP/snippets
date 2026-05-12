---
tags: ["python", "tools", "gcode", "3d-printing"]
---
# G-code Post-processing Runner (Python)

Master script that runs a chain of G-code post-processing scripts after slicing (e.g. from PrusaSlicer). Each sub-script receives the output of the previous one. Designed for Prusa printers but adaptable to any slicer that supports a post-processing command.

## Dependencies

No third-party packages required — uses `subprocess`, `os`, `logging` from the standard library.

## Usage

Configure the paths in the script, then point your slicer's post-processing command to it:

```
python3 /path/to/post_process_master.py
```

In PrusaSlicer: *Print Settings → Output options → Post-processing scripts*

## Code

```python
import os
import subprocess
import logging
import traceback

# --- Configuration ---
SCRIPTS_DIR = "/home/user/prusa/scripts"
LOG_FILE    = "/home/user/prusa/post_process_master.log"

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
    """Prepend bed and nozzle wait commands to the G-code file."""
    temp_commands = [
        "M190 S65 ; Wait for bed 65°C\n",
        "M109 S210 ; Wait for nozzle 210°C\n",
    ]
    with open(gcode_file, "r") as f:
        lines = f.readlines()
    with open(gcode_file, "w") as f:
        f.writelines(temp_commands + lines)
    logger.info("Temperature commands prepended.")


def run_script(script_name: str, input_file: str, output_file: str) -> None:
    """Run a single post-processing script."""
    script_path = os.path.join(SCRIPTS_DIR, script_name)
    cmd = ["python3", script_path, input_file, output_file]
    logger.info(f"Running: {' '.join(cmd)}")
    subprocess.check_call(cmd)
    logger.info(f"{script_name} completed.")


def main(gcode_file: str) -> None:
    try:
        add_temperature_commands(gcode_file)

        current_input = gcode_file
        for script in PIPELINE:
            base, ext = os.path.splitext(gcode_file)
            output = f"{base}_{script.replace('.py', '')}{ext}"
            run_script(script, current_input, output)
            current_input = output

        logger.info("All post-processing scripts finished.")

    except Exception as e:
        logger.error(f"Pipeline failed: {e}")
        traceback.print_exc()


if __name__ == "__main__":
    import sys
    if len(sys.argv) < 2:
        print("Usage: python3 post_process_master.py <file.gcode>")
        sys.exit(1)
    main(sys.argv[1])
```
