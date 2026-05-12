---
tags: ["shell-linux", "system", "network", "nc", "port", "test"]
---
# Test IP / Port Reachability

Checks whether a host is reachable on a specific port from Linux, Windows, or Python.

Paste and run directly in the terminal — no file needed.

## Command

### Linux — netcat

```bash
nc -vz 192.168.1.100 8080
```

> Exits with code `0` if the port is open, `1` if refused or timed out. Add `-w 3` to set a 3-second timeout.

### Linux — curl

```bash
curl -v telnet://192.168.1.100:8080
```

### Windows — PowerShell

```powershell
Test-NetConnection -ComputerName 192.168.1.100 -Port 8080
```

---

## Python

### Check if a URL responds (HTTP)

```python
import requests

def is_reachable(url: str, timeout: float = 5.0) -> bool:
    try:
        resp = requests.head(url, allow_redirects=True, timeout=timeout)
        return resp.status_code < 400
    except requests.RequestException:
        return False

print(is_reachable("http://192.168.1.100:8080"))
```

### Validate IP and port format before connecting

```python
import socket

def validate_ip_port(ip: str, port: int) -> bool:
    try:
        socket.inet_aton(ip)
    except socket.error:
        return False
    return 0 < port <= 65535
```
