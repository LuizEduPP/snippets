---
tags: ["shell-windows", "wsl", "filesystem"]
---
# Access WSL Filesystem from Windows

Navigates to the Linux filesystem of a WSL distribution from Windows Explorer or PowerShell — and vice versa.

## Command

### Open WSL filesystem in Windows Explorer

Type this path directly in the Explorer address bar:

```
\\wsl$\
```

This lists all installed distributions. To go directly into one:

```
\\wsl$\Ubuntu
```

### Open current WSL directory in Windows Explorer (from inside WSL)

```bash
explorer.exe .
```

### Open a Windows path from inside WSL

```bash
cd /mnt/c/Users/YourName/Desktop
```

Windows drives are mounted under `/mnt/` — C: becomes `/mnt/c`, D: becomes `/mnt/d`, etc.

### Open WSL terminal directly into a Windows folder (from PowerShell)

```powershell
wsl --cd "C:\Users\YourName\Projects"
```
