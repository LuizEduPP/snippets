---
tags: ["shell-linux", "system", "tomcat", "logs", "java"]
---
# View Tomcat Logs (Linux / Windows)

Tails and searches Apache Tomcat logs to debug startup failures, deployment errors, and runtime exceptions.

Paste and run directly in the terminal — no file needed.

## Command

### Linux — live tail

```bash
tail -f /var/log/tomcat/catalina.out
```

### Linux — search for errors

```bash
grep -i "error\|exception\|failed" /var/log/tomcat/catalina.out
```

### Linux — check log size

```bash
du -sh /var/log/tomcat/
ls -lh /var/log/tomcat/
```

### Linux — last 100 lines

```bash
tail -n 100 /var/log/tomcat/catalina.out
```

---

## Windows — PowerShell

```powershell
# Tail the log (equivalent of tail -f)
Get-Content "C:\tomcat\logs\catalina.out" -Wait

# Search for errors
Select-String -Path "C:\tomcat\logs\catalina.out" -Pattern "error|exception" -CaseSensitive:$false
```

---

## Rotate / clear logs

```bash
# Truncate without deleting (Tomcat must be running)
sudo truncate -s 0 /var/log/tomcat/catalina.out

# Or remove old rotated logs
sudo find /var/log/tomcat/ -name "*.log.*" -mtime +7 -delete
```

---

## Notes

- Default Linux path may vary: `/opt/tomcat/logs/catalina.out` or `/usr/share/tomcat*/logs/`.
- Tomcat also creates `localhost.YYYY-MM-DD.log`, `manager.YYYY-MM-DD.log` in the same folder.
- Use `journalctl -u tomcat -f` if Tomcat runs as a systemd service.
