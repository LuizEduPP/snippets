---
tags: ["bash", "system", "xdg", "file-manager", "dolphin"]
---
# Set Default File Manager (Linux)

Forces standard Linux UI environments to open raw folder directives via a specified primary file explorer using native XDG MIME specifications.

## 🛠️ How it works under the hood

1. **`xdg-mime` protocol**: Linux doesn't track default file types via a pure Windows-like registry. Instead, it relies on XDG (Cross-Desktop Group) MIME logic. When an app requests to open a folder path, it sends an `inode/directory` MIME request. Setting this locally maps that MIME type directly to the executed `.desktop` application limits.

---

## 🚀 Usage Guide

### 1. Install Target Dependencies
Ensure the GUI application actually exists inside system boundaries.
```bash
# Ubuntu/Zorin
sudo apt install dolphin

# Arch/Manjaro
sudo pacman -S dolphin
```

### 2. Lock XDG MIME Pointers
Configure the literal default `.desktop` app targeted by system requests.
```bash
# Register Dolphin (KDE Base)
xdg-mime default dolphin.desktop inode/directory
xdg-mime default dolphin.desktop application/x-directory

# Register Nautilus (GNOME Base)
xdg-mime default nautilus.desktop inode/directory

# Register Thunar (Xfce Base)
xdg-mime default thunar.desktop inode/directory
```

### 3. Verify Execution Maps
Query the local boundary to confirm the XDG mapping succeeded. ```bash
xdg-mime query default inode/directory
```
