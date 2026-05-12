---
tags: ["bash", "network", "nc", "port", "test", "python", "windows"]
---
# Test IP / Port Reachability

Checks whether a host is reachable on a specific port from Linux terminals, Windows PowerShell instances, or Python scripts.

## 🛠️ How it works under the hood

1. **`netcat` (`nc`)**: Acts as a raw network backend, resolving low-level TCP/UDP socket handshakes without sending application-layer payload data. 2. **`Test-NetConnection`**: The Windows PowerShell equivalent for initiating localized OS TCP packets.
3. **Python `requests` / `socket`**: Initiates identical TCP connections via language-level abstractions mapped directly to network layers.

---

## 🚀 Usage Guide

### 1. Execute Command Line Testing (Linux)

**Using netcat (nc)**
```bash
nc -vz 192.168.1.100 8080
```
> Exits with code `0` if the port is open, `1` if refused or timed out. Add `-w 3` to set a 3-second timeout limit.

**Using curl**
```bash
curl -v telnet://192.168.1.100:8080
```

### 2. Execute Command Line Testing (Windows)

Launch inside PowerShell.
```powershell
Test-NetConnection -ComputerName 192.168.1.100 -Port 8080
```

### 3. Check State using Python

Use standard native libraries checking URL reachability through HEAD requests.
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

Use `socket` limits parsing fundamental configurations without sending payloads.
```python
import socket

def validate_ip_port(ip: str, port: int) -> bool:
 try:
 socket.inet_aton(ip)
 except socket.error:
 return False
 return 0 < port <= 65535
```
