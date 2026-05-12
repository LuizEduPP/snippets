---
tags: ["bash", "system", "flatpak", "packages", "ui"]
---
# Flatpak — Install, Run, and Override Environment

Manages standard Flatpak sandboxed applications, overrides graphical environment variables for Wayland/X11 compatibility, and clears out orphaned runtimes.

## 🛠️ How it works under the hood

1. **Bubblewrap Sandboxing**: Flatpak uses `bwrap` to isolate applications into confined Linux containers. Each app gets its own specific runtime (libraries like KDE or GNOME) separate from the host system.
2. **Environment Overrides**: Sometimes the default graphical backend (like native Wayland) breaks legacy apps. The `override` directive bypasses the strict sandbox barriers, forcing explicit GTK or GDK variables across the runtime boundaries.

---

## 🚀 Usage Guide

### 1. Basic Lifecycle
```bash
# Install an app
flatpak install flathub com.example.AppName

# Run an app
flatpak run com.example.AppName

# Clean up orphaned runtimes to save space
flatpak uninstall --unused
```

### 2. Fix Display Issues (Wayland to X11 Fallback)
Force legacy apps to use X11 instead of Wayland.
```bash
# Fix missing window buttons/borders on a specific app
flatpak override com.example.AppName --env=GDK_BACKEND=x11 --env=GTK_CSD=0

# Apply override globally to all user apps
flatpak override --user --env=GTK_CSD=0 --env=GDK_BACKEND=x11
```
