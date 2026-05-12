---
tags: ["shell-linux", "system", "klipper", "3d-printing"]
---
# Switch Klipper Printer Configuration

Swaps the active printer config in Klipper without rebooting — useful when managing multiple 3D printers from the same Raspberry Pi.

Paste and run directly in the terminal — no file needed.

## Command

### Stop Klipper, swap config, restart

```bash
# Stop Klipper
sudo service klipper stop

# Copy the desired printer config
cp ~/klipper_config/ender5.cfg ~/printer.cfg

# Start Klipper with the new config
sudo service klipper start
```

> Keep each printer's config as a separate file: `~/klipper_config/ender3.cfg`, `ender5.cfg`, etc.  
> Replace `ender5.cfg` with the config you want to activate.

---

## Multi-instance Moonraker (two printers simultaneously)

### Check which ports each instance is using

```bash
netstat -tulnp | grep moonraker
```

> Default: `7125` for instance 1, `7126` for instance 2.

### Start a second Moonraker instance

```bash
sudo systemctl start moonraker@instance2
```

### Configure each instance

Edit `/etc/moonraker-instance2.conf` (or equivalent) and set:

```ini
[server]
instance_name: Ender5S1
```

vs the first instance:

```ini
[server]
instance_name: Ender3Pro
```
