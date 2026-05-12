---
tags: ["python", "network", "ip", "port", "socket"]
---
# Validate IP Address and Port (Python)

Checks whether a string is a valid IPv4 address, whether a port number is in range, and whether a host is accepting TCP connections on that port.

## 🛠️ How it works under the hood

1. **`socket.inet_aton()`**: Tries to parse an IP string into its 4-byte binary form. If the string is malformed (e.g., `999.0.0.1` or `not-an-ip`), it raises `socket.error`, which is caught to signal an invalid address.
2. **`socket.connect_ex()`**: Opens a TCP socket and attempts a full handshake with `(host, port)`. Unlike `connect()`, it returns an integer error code instead of raising — `0` means the port is open and accepted the connection; anything else means closed or unreachable.
3. **`requests.head()`**: Sends an HTTP HEAD request to a URL — no response body is downloaded, only headers. A status code below 400 confirms the server is alive.

---

## 🚀 Usage Guide

### 1. Install dependencies
```bash
pip install requests
```

### 2. Complete script
```python
import socket
import requests

# ── Validators ────────────────────────────────────────────────────────────────

def is_valid_ip(ip: str) -> bool:
    """Returns True if the string is a valid IPv4 address."""
    try:
        socket.inet_aton(ip)
        return True
    except socket.error:
        return False

def is_valid_port(port: int) -> bool:
    """Returns True if the port is in the valid TCP/UDP range (1–65535)."""
    return isinstance(port, int) and 1 <= port <= 65535

# ── Connectivity checks ───────────────────────────────────────────────────────

def is_port_open(host: str, port: int, timeout: float = 3.0) -> bool:
    """Returns True if the TCP port is accepting connections."""
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        return s.connect_ex((host, port)) == 0

def is_url_reachable(url: str, timeout: float = 5.0) -> bool:
    """Returns True if the URL returns an HTTP status below 400."""
    try:
        resp = requests.head(url, allow_redirects=True, timeout=timeout)
        return resp.status_code < 400
    except requests.RequestException:
        return False

# ── Main ──────────────────────────────────────────────────────────────────────

if __name__ == "__main__":
    ip = "192.168.1.100"
    port = 8080

    if not is_valid_ip(ip):
        print(f"Invalid IP address: {ip}")
    elif not is_valid_port(port):
        print(f"Invalid port: {port}")
    elif is_port_open(ip, port):
        print(f"{ip}:{port} is open")
    else:
        print(f"{ip}:{port} is closed or unreachable")

    # HTTP check example
    url = "http://192.168.1.100:8080"
    print(f"{url} reachable: {is_url_reachable(url)}")
```
