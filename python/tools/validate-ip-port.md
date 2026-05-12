---
tags: ["python", "tools", "network", "ip", "port", "socket"]
---
# Validate IP Address and Port (Python)

Validates an IPv4 address and port number using the standard library, and optionally checks if an HTTP URL is reachable with `requests`.

## Dependencies

```bash
pip install requests
```

## Code

### Validate IP and port format

```python
import socket

def is_valid_ip(ip: str) -> bool:
    """Returns True if the string is a valid IPv4 address."""
    try:
        socket.inet_aton(ip)
        return True
    except socket.error:
        return False

def is_valid_port(port: int) -> bool:
    """Returns True if port is in the valid range (1–65535)."""
    return isinstance(port, int) and 1 <= port <= 65535
```

### Check if an IP:port is open

```python
import socket

def is_port_open(host: str, port: int, timeout: float = 3.0) -> bool:
    """Returns True if the TCP port is accepting connections."""
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        return s.connect_ex((host, port)) == 0
```

### Check if an HTTP URL is reachable

```python
import requests

def is_url_reachable(url: str, timeout: float = 5.0) -> bool:
    """Returns True if the URL responds with HTTP < 400."""
    try:
        resp = requests.head(url, allow_redirects=True, timeout=timeout)
        return resp.status_code < 400
    except requests.RequestException:
        return False
```

### Combined usage

```python
ip = "192.168.1.100"
port = 8080

if is_valid_ip(ip) and is_valid_port(port):
    if is_port_open(ip, port):
        print(f"{ip}:{port} is open")
    else:
        print(f"{ip}:{port} is closed or unreachable")
else:
    print("Invalid IP or port")
```
