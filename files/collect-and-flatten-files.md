---
tags: ["linux", "files", "find", "flatten", "automation"]
---
# Collect and Flatten Code Files for LLM Context

This script walks through all subdirectories, reads specific code files (like `.py`, `.js`, etc.), removes indentation and blank lines, collapses each file into a single continuous line, and appends everything into a single, timestamped output text file.

This is highly useful when you need to condense a large codebase to paste it into an LLM (like ChatGPT or Claude) without exceeding token limits constraints.

## 🛠️ How it works under the hood

Instead of running a giant, unreadable one-liner, here is a breakdown of what happens:

1. **`find. -name "*.py"`**: Searches for all Python files recursively starting from the current directory.
2. **`while read -r file`**: Loops through every file found in the previous step.
3. **`sed -e 's/^[[:space:]]*//' -e '/^$/d' "$file"`**: 
 - `s/^[[:space:]]*//`: Removes leading whitespace (indentation) from each line.
 - `/^$/d`: Deletes completely blank lines.
4. **`tr -d '\n'`**: Deletes all newline characters, joining all lines of a file into a single line.
5. **`sed 's/$/ /'`**: Adds a single space at the end of the flattened line so it doesn't merge directly into the next file block.
6. **`>> "$OUTPUT"`**: Appends the processed content into the dynamically generated text file.

---

## 🚀 Quick Usage

Just copy and paste the command below into your terminal at the root of your project.

### Recursive (All Subdirectories)

```bash
OUTPUT="code_$(date +%Y%m%d_%H%M%S)_$RANDOM.txt"; \
find. -name "*.py" | sort | while read -r file; do \
 echo -e "\n### FILE: $file ###" >> "$OUTPUT"; \
 sed -e 's/^[[:space:]]*//' -e '/^$/d' "$file" | tr -d '\n' | sed 's/$/ /' >> "$OUTPUT"; \
done; \
echo "✅ Finished! Output saved to: $OUTPUT"
```

*Note: You can easily change `*.py` to `*.ts`, `*.js`, or `*.md` to target a different programming language.*

## 📋 Example Output

Inside the generated `code_20231027_153045_12345.txt` file, you will find:

```text
### FILE: module/script.py ###
import os def main(): pass x = 1...

### FILE: utils/helpers.py ###
import re def clean(s): return s.strip()...
```
