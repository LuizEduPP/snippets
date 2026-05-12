---
tags: ["shell-linux", "system", "kde", "ubuntu", "install"]
---
# Install KDE Plasma on Ubuntu / Zorin OS

Adds the KDE Plasma desktop environment alongside the existing GNOME/Zorin desktop, selectable at the login screen.

Paste and run directly in the terminal — no file needed.

## Command

### Full KDE Plasma desktop

```bash
sudo apt update
sudo apt install kde-plasma-desktop
```

### Minimal install (fewer default apps)

```bash
sudo apt install kde-plasma-desktop --no-install-recommends
```

### Full KDE suite (Plasma + all KDE apps)

```bash
sudo apt install kde-full
```

---

## After installation

1. **Log out** of the current session.
2. At the login screen, click the **gear icon** next to your username.
3. Select **Plasma** and log in.

---

## Remove KDE Plasma (revert)

```bash
sudo apt remove --purge kde-plasma-desktop kde-full
sudo apt autoremove
```

---

## Notes

- Installing Plasma alongside GNOME/Zorin may cause theme conflicts and duplicate apps (e.g., two file managers, two terminal apps).
- Additional Qt libraries will be installed as dependencies — these are shared with GTK apps and generally safe.
- For a cleaner experience, consider installing Kubuntu or KDE Neon instead of mixing desktops.
