---
tags: ["shell-linux", "files", "css", "reset"]
---
# Reset All CSS Files with Empty Selectors

Overwrites every `.css` file in the current directory with an empty rule block using the filename (without extension) as the selector.

**Before:**
```
button.css   →  (any content)
card.css     →  (any content)
navbar.css   →  (any content)
```

**After:**
```
button.css   →  button {}
card.css     →  card {}
navbar.css   →  navbar {}
```

> **Warning:** this overwrites file content. Make sure you have a backup or are working in a clean directory.

## Usage

```bash
for f in *.css; do echo "${f%.css} {}" > "$f"; done
```

## Variants

Keep existing content and append the empty block instead of overwriting:

```bash
for f in *.css; do echo "${f%.css} {}" >> "$f"; done
```

Target a specific directory:

```bash
for f in /path/to/styles/*.css; do echo "${f##*/}" | sed 's/\.css/ {}/' > "$f"; done
```
