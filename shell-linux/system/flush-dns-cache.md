---
tags: ["shell-linux", "system", "dns", "network", "cache"]
---
# Flush DNS Cache

Clears the local DNS cache on Linux and Windows to resolve stale records, name resolution failures, and connection issues after changing DNS settings.

Paste and run directly in the terminal — no file needed.

## Command

### Linux — systemd-resolved

```bash
sudo systemd-resolve --flush-caches

# Verify stats
sudo resolvectl status
```

### Linux — NetworkManager (restart)

```bash
sudo systemctl restart NetworkManager
```

### Linux — nscd (if installed)

```bash
sudo systemctl restart nscd
```

---

## Windows (cmd or PowerShell)

```cmd
ipconfig /flushdns
ipconfig /renew
```

---

## Change DNS server (Linux — NetworkManager)

```bash
# Set DNS for a connection
nmcli connection modify "CONNECTION_NAME" ipv4.dns "1.1.1.1 8.8.8.8"
nmcli connection up "CONNECTION_NAME"
```

## Set DNS via /etc/resolv.conf (temporary)

```bash
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf
```

---

## Test DNS resolution

```bash
# Query a domain
dig google.com

# Quick check
nslookup google.com

# Show which DNS server is used
resolvectl query google.com
```
