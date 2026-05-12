---
tags: ["bash", "system", "gtk", "qt"]
---
# List GTK/Qt Binaries in /usr/bin

A robust system analysis script that scans underlying executable shared libraries via `ldd` and prints explicit environment linkages determining whether software relies on GTK or Qt environments.

## 🛠️ How it works under the hood

1. **`ldd` command**: Exposes structural linkages dynamically. Every compiled binary relies on shared object layers (`.so`). `ldd "$bin"` grabs these raw links mapped into `/usr/lib/`.
2. **`grep libgtk` vs `libQt`**: GTK programs inherently attach to `libgtk-3.so` or `libgtk-4.so`. KDE or Qt programs link to `libQt5Core.so` or `libQt6Core.so`. We pipe the linkages through `grep` to tag the binaries. ---

## 🚀 Usage Guide

### Expected Script Output
```
[GTK] /usr/bin/gedit
[GTK] /usr/bin/nautilus
[Qt ] /usr/bin/dolphin
[Qt ] /usr/bin/konsole
```

### Full Environmental Scan
Finds all executables and labels them dynamically depending on matching pipelines.
```bash
for bin in /usr/bin/*; do
 [[ -x "$bin" && ! -d "$bin" ]] || continue
 libs=$(ldd "$bin" 2>/dev/null)
 echo "$libs" | grep -q "libgtk" && echo "[GTK] $bin"
 echo "$libs" | grep -q "libQt" && echo "[Qt ] $bin"
done
```

### Isolate GTK binaries exclusively
```bash
for bin in /usr/bin/*; do
 [[ -x "$bin" && ! -d "$bin" ]] || continue
 ldd "$bin" 2>/dev/null | grep -q "libgtk" && echo "[GTK] $bin"
done
```

### Isolate Qt binaries exclusively
```bash
for bin in /usr/bin/*; do
 [[ -x "$bin" && ! -d "$bin" ]] || continue
 ldd "$bin" 2>/dev/null | grep -q "libQt" && echo "[Qt ] $bin"
done
```
