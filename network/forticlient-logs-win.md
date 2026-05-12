---
tags: ["powershell", "windows", "forticlient", "logs", "vpn"]
---
# View FortiClient VPN Logs (Windows)

Parses local filesystem boundaries tracking FortiClient VPN arrays to expose raw string values mapping to failed tunnel handshakes immediately without GUI limits.

## 🛠️ How it works under the hood

1. **Powershell Target Piping**: Standard `Get-Content -Wait` acts identically to UNIX `tail -f`, pushing pure raw I/O text updates internally directly. Using `Select-String` safely traps Regex logic directly over specific target exceptions.

---

## 🚀 Usage Guide

### 1. Identify Target Node Locations
```text
C:\ProgramData\Fortinet\FortiClient\logs\
C:\Program Files\Fortinet\FortiClient\logs\
```

### 2. Tail Stream Limit Native Outputs
Run inside a clean Powershell window inherently.
```powershell
Get-Content "C:\ProgramData\Fortinet\FortiClient\logs\FortiClient.log" -Wait
```

### 3. Trap Fault Limits Separately
Isolate clean string matches directly over failure connections inherently.
```powershell
Select-String -Path "C:\ProgramData\Fortinet\FortiClient\logs\FortiClient.log" -Pattern "error|fail|disconnect" -CaseSensitive:$false
```

### 4. Search File Bounds Completely
```powershell
Get-ChildItem "C:\ProgramData\Fortinet\FortiClient\logs\" -Recurse
```
