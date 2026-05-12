---
tags: ["windows", "wsl", "filesystem", "navigation"]
---
# Access the WSL Linux Filesystem from Windows

If you are running Windows Subsystem for Linux (WSL), the virtual environment uses its own closed EXT4 filesystem, normally insulated from Windows. 

This guide reveals native pathways to cross the boundary : accessing your `Ububtu/Linux` files from Windows tools like File Explorer, and accessing your `Windows C:` drive from inside the Linux terminal.

## 🛠️ How it works under the hood

1. **`\\wsl$\`**: Microsoft built a synthetic network path (a UNC protocol share pointer) embedded in the Windows kernel. Any system process (like File Explorer) reading this bridge asks WSL for the filesystem chunks.
2. **`/mnt/c/`**: Conversely, inside the Linux bash terminal, Microsoft overrides standard Linux mount mappings to inject your standard `C:\` and `D:\` drives straight into the UNIX root under `/mnt/`.

---

## 🚀 Usage Guide

### 1. Open WSL Linux files inside Windows Explorer Do not try to find the hidden virtual disk! Type this specialized network path exactly as written into the top address bar of Windows File Explorer to see all your active distributions:

```text
\\wsl$\
```

If your standard distribution is Ubuntu, jump directly to its Linux Root `/` folder using:

```text
\\wsl$\Ubuntu
```
*Note: From here, you can safely copy or modify Linux files using standard Windows software such as VS Code.*

### 2. View current WSL directory as a Windows Interface
If you are currently inside your Linux terminal (i.e. deeply embedded inside a project at `/home/user/project_X`) and you suddenly need to see those files inside a Windows folder, execute the Windows File Explorer executable directly from Bash:

```bash
explorer.exe.
```
*(The dot `.` tells Explorer to open the path you are currently standing in).*

---

## 💡 Accessing Windows from inside Linux

### 3. Modifying Windows files from Bash
If you need to access your typical Windows Desktop or Documents folder to run standard Linux Git or Bash commands on them, simply cross the boundary through the `/mnt/` mount points.

```bash
cd /mnt/c/Users/YourName/Desktop
```

Any Windows drives you possess drop the colon `:` and are structurally mirrored here (`C:` is `/mnt/c`, `D:` is `/mnt/d`, etc).

### 4. Jump WSL Terminal into a Windows Path immediately
If you have a PowerShell window open directly targeting a normal Windows-level project pathway (e.g. `C:\Users\YourName\Projects`), and you suddenly decide you need Linux commands, wrap the WSL executable command via the `--cd` flag:

```powershell
wsl --cd "C:\Users\YourName\Projects"
```
