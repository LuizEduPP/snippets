---
tags: ["bash", "system", "pacman", "arch", "manjaro", "packages"]
---
# Pacman Cleanup (Arch / Manjaro)

Cleans isolated dependency chains, removes orphaned packages, and purges the core `pacman` cache directory to reclaim large sectors of disk space locally.

## 🛠️ How it works under the hood

1. **Orphans (`-Qdt`)**: When Arch systems upgrade modules, core packages leave behind abandoned libraries that are no longer strictly required by installed executables. 
2. **Pacman Caching (`/var/cache/pacman/pkg`)**: Arch downloads full `.pkg.tar.zst` payload structures before uncompressing them locally. Pacman inherently keeps every downloaded module forever in the cache directory, requiring manual deletion.

---

## 🚀 Usage Guide

### 1. Execute Dependency Synchronization
Always make sure headers are updated before resolving removals.
```bash
sudo pacman -Syu
```

### 2. Isolate and Purge Orphan Targets
```bash
# Query the system to view what objects are orphaned
pacman -Qdt

# pass the query into the purge pipeline
sudo pacman -Rns $(pacman -Qdtq)
```

### 3. Flush the Module Caches
```bash
# Safely clear the cache, keeping only the 3 most recent backups
paccache -r

# Or, use pacman to nuke ALL disabled packages instantly
sudo pacman -Sc

# Nuke everything from the cache directory (Extreme)
sudo pacman -Scc
```
