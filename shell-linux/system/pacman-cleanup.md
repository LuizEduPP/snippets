---
tags: ["shell-linux", "system", "pacman", "arch", "manjaro", "packages"]
---
# Pacman Cleanup (Arch / Manjaro)

Removes orphaned packages and clears the package cache to reclaim disk space on Arch-based distros.

Paste and run directly in the terminal — no file needed.

## Command

### Update all packages

```bash
sudo pacman -Syu
```

### List orphaned packages (no longer needed)

```bash
pacman -Qdt
```

### Remove all orphaned packages

```bash
sudo pacman -Rns $(pacman -Qdtq)
```

### Clear old package cache (keep last 3 versions)

```bash
sudo pacman -Sc
```

### Clear ALL cached packages

```bash
sudo pacman -Scc
```

---

## Notes

- `-R` removes the package; `-n` skips `.pacsave` backup files; `-s` also removes unneeded dependencies recursively.
- Use `paccache -r` (from `pacman-contrib`) for a safer cache cleanup that keeps the 3 most recent versions automatically.
- On Manjaro, prefer **Pamac** or `pamac clean` as a GUI alternative.
