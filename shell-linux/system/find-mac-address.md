---
tags: ["shell-linux", "system", "network", "mac-address", "arp"]
---
# Find MAC Address

Shows the MAC address of network interfaces and of devices on the local network.

Paste and run directly in the terminal — no file needed.

## Command

### Your own interfaces

```bash
# Linux
ip link show

# macOS
ifconfig | grep ether

# Windows (CMD)
ipconfig /all
```

### Devices on the local network (ARP table)

```bash
# Linux / macOS
ip neigh

# Windows (CMD)
arp -a
```

> The ARP table only shows devices that have communicated with your machine recently. Run a ping sweep first to populate it:

```bash
# Linux — ping the whole /24 subnet
for i in $(seq 1 254); do ping -c1 -W1 192.168.1.$i &>/dev/null & done; sleep 2; ip neigh
```
