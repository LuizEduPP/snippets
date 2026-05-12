---
tags: ["shell-linux", "system", "gtk", "qt"]
---
# List GTK/Qt Binaries in /usr/bin

Scans all executables in `/usr/bin` and shows which ones link against **GTK** or **Qt**.

Paste and run directly in the terminal — no file needed.

## Expected output

```
[GTK] /usr/bin/gedit
[GTK] /usr/bin/nautilus
[Qt ] /usr/bin/dolphin
[Qt ] /usr/bin/konsole
```

## Show everything (GTK + Qt)

```bash
for bin in /usr/bin/*; do
  [[ -x "$bin" && ! -d "$bin" ]] || continue
  libs=$(ldd "$bin" 2>/dev/null)
  echo "$libs" | grep -q "libgtk" && echo "[GTK] $bin"
  echo "$libs" | grep -q "libQt" && echo "[Qt ] $bin"
done
```

## GTK only

```bash
for bin in /usr/bin/*; do
  [[ -x "$bin" && ! -d "$bin" ]] || continue
  ldd "$bin" 2>/dev/null | grep -q "libgtk" && echo "[GTK] $bin"
done
```

## Qt only

```bash
for bin in /usr/bin/*; do
  [[ -x "$bin" && ! -d "$bin" ]] || continue
  ldd "$bin" 2>/dev/null | grep -q "libQt" && echo "[Qt ] $bin"
done
```
