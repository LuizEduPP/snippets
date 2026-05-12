---
tags: ["shell-linux", "files", "find", "flatten"]
---
# Collect and Flatten Python Files into a Single Text File

Walks through all subdirectories, reads every `.py` file, strips indentation and blank lines, collapses each file to a single line, and appends everything to a timestamped output file.

Useful for feeding a codebase into an LLM prompt or creating a compact snapshot.

Paste and run directly in the terminal from your project root — no script file needed.

## Output format

```
### FILE: module/script.py ###
import os def main(): pass ...

### FILE: utils/helpers.py ###
import re def clean(s): return s.strip() ...
```

Output file example: `code_20231027_153045_12345.txt`

## One directory deep

```bash
OUTPUT="code_$(date +%Y%m%d_%H%M%S)_$RANDOM.txt"; for file in */*.py; do echo "### FILE: $file ###" >> "$OUTPUT"; sed -e 's/^[[:space:]]*//' -e '/^$/d' "$file" | tr -d '\n' | sed 's/$/ /' >> "$OUTPUT"; echo -e "\n" >> "$OUTPUT"; done; echo "Output file: $OUTPUT"
```

## All depths (recursive)

```bash
OUTPUT="code_$(date +%Y%m%d_%H%M%S)_$RANDOM.txt"; find . -name "*.py" | sort | while read -r file; do echo "### FILE: $file ###" >> "$OUTPUT"; sed -e 's/^[[:space:]]*//' -e '/^$/d' "$file" | tr -d '\n' | sed 's/$/ /' >> "$OUTPUT"; echo -e "\n" >> "$OUTPUT"; done; echo "Output file: $OUTPUT"
```

Change `*.py` to any other extension (e.g. `*.ts`, `*.js`) to target a different language.
