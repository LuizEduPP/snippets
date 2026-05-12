---
tags: ["shell-windows", "network", "port", "process", "kill"]
---
# Kill Process on Port (Windows CMD)

Finds and terminates the process occupying a specific port. Run CMD as Administrator.

## Command

### Step 1 — Find the PID

Replace `8080` with your port number.

```cmd
netstat -ano | findstr :8080
```

Look for a line with `LISTENING` and note the last number (the PID):
```
TCP    0.0.0.0:8080    0.0.0.0:0    LISTENING    12345
```

### Step 2 — Kill the process

Replace `12345` with the PID from the previous step.

```cmd
taskkill /PID 12345 /F
```

---

## If the state shows `TIME_WAIT` with PID 0

The process already exited — Windows is holding the port temporarily. It clears on its own in a few minutes, or you can force it by restarting the NAT driver:

```cmd
net stop winnat
net start winnat
```
