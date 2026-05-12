---
tags: ["shell-linux", "system", "network", "port", "process", "kill"]
---
# Kill Process on Port (Linux)

Identifies and terminates the process occupying a specific TCP port using `fuser`.

Paste and run directly in the terminal — no file needed.

## Command

Replace `8080` with your port number.

### Check which process is using the port

```bash
sudo fuser 8080/tcp
```

### Show process name alongside the PID

```bash
sudo fuser -v 8080/tcp
```

### Kill the process directly

```bash
sudo fuser -k 8080/tcp
```
