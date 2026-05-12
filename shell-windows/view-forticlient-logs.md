---
tags: ["shell-windows", "forticlient", "logs", "vpn"]
---
# View FortiClient VPN Logs (Windows)

Locates and tails the FortiClient log file on Windows to diagnose VPN connection failures, authentication errors, or tunnel drops.

Paste and run directly in the terminal — no file needed.

## Command

### Default log paths

```
C:\ProgramData\Fortinet\FortiClient\logs\
C:\Program Files\Fortinet\FortiClient\logs\
```

### Tail the log in real time (PowerShell)

```powershell
Get-Content "C:\ProgramData\Fortinet\FortiClient\logs\FortiClient.log" -Wait
```

### Search for errors

```powershell
Select-String -Path "C:\ProgramData\Fortinet\FortiClient\logs\FortiClient.log" -Pattern "error|fail|disconnect" -CaseSensitive:$false
```

### List all log files

```powershell
Get-ChildItem "C:\ProgramData\Fortinet\FortiClient\logs\" -Recurse
```

---

## Notes

- `Get-Content -Wait` is the PowerShell equivalent of `tail -f` on Linux.
- If the `ProgramData` folder is hidden, run `attrib -h C:\ProgramData` or enable hidden items in File Explorer.
- FortiClient EMS managed clients may restrict log access — check with your IT admin.
