---
tags: ["shell-linux", "system", "flatpak", "packages"]
---
# Flatpak — Install, Run, and Override Environment

Common Flatpak commands for installing apps, overriding environment variables, and fixing display issues on Wayland.

Paste and run directly in the terminal — no file needed.

## Command

### Add Flathub repository

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### Install, run, and uninstall an app

```bash
# Install
flatpak install flathub com.example.AppName

# Run
flatpak run com.example.AppName

# Uninstall
flatpak uninstall com.example.AppName

# Remove unused runtimes
flatpak uninstall --unused
```

### List installed apps

```bash
# Apps only
flatpak list --app

# With app ID and origin
flatpak list --app --columns=application,origin
```

---

## Fix display / buttons on Wayland

Override environment variables to force X11 mode:

```bash
# For a single app
flatpak override com.example.AppName --env=GDK_BACKEND=x11 --env=GTK_CSD=0

# For all user apps
flatpak override --user --env=GTK_CSD=0 --env=GDK_BACKEND=x11

# Revert all overrides
flatpak override --user --reset
```

---

## Update all apps

```bash
flatpak update
```

## Check app permissions

```bash
flatpak info --show-permissions com.example.AppName
```
