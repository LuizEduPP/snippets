---
tags: ["shell-linux", "system", "clipboard", "xclip"]
---
# Clipboard Commands with xclip

Copies and pastes text to/from the system clipboard in the terminal using `xclip`.

Paste and run directly in the terminal — no file needed.

## Install

```bash
# Debian/Ubuntu
sudo apt install xclip

# Arch/Manjaro
sudo pacman -S xclip

# Fedora
sudo dnf install xclip
```

## Command

### Copy command output to clipboard

```bash
echo "text" | xclip -selection clipboard
```

### Copy file contents to clipboard

```bash
cat file.txt | xclip -selection clipboard
```

### Paste clipboard content to a file

```bash
xclip -o -selection clipboard > file.txt
```

### Copy to primary clipboard (mouse middle-click)

```bash
echo "text" | xclip -selection primary
```

---

## Aliases (add to `~/.bashrc` or `~/.zshrc`)

```bash
# Copy to clipboard
alias ccp='xclip -selection clipboard'

# Paste from clipboard
alias cvp='xclip -o -selection clipboard'

# Copy file to clipboard
alias ccpf='xclip -selection clipboard <'
```

Usage after sourcing:

```bash
cat myfile.txt | ccp     # copy
cvp                      # paste
ccpf report.md           # copy file
```

---

> On Wayland, replace `xclip` with `wl-copy` / `wl-paste` from the `wl-clipboard` package.
