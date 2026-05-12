---
tags: ["shell-linux", "system", "cron", "curl", "schedule"]
---
# Schedule a URL Request with Cron

Sends an HTTP request to a URL on a recurring schedule using `curl` and crontab. Useful for keeping services alive, triggering webhooks, or periodic health checks.

Paste and run directly in the terminal — no file needed.

## Command

### Open crontab editor

```bash
crontab -e
```

### Add a schedule entry

Replace the URL with your target. The example below runs every hour, on the hour.

```bash
# Every hour (at minute 0)
0 * * * * curl -s "https://example.com/ping" > /dev/null 2>&1
```

```bash
# Every hour from boot (alternative shorthand)
@hourly curl -s "https://example.com/ping" > /dev/null 2>&1
```

```bash
# Every 30 minutes
*/30 * * * * curl -s "https://example.com/ping" > /dev/null 2>&1
```

```bash
# Once a day at 8 AM
0 8 * * * curl -s "https://example.com/ping" > /dev/null 2>&1
```

### List active jobs

```bash
crontab -l
```

---

## Cron field reference

```
┌─ minute   (0–59)
│ ┌─ hour   (0–23)
│ │ ┌─ day  (1–31)
│ │ │ ┌─ month (1–12)
│ │ │ │ ┌─ weekday (0–7, 0 and 7 = Sunday)
│ │ │ │ │
* * * * *  command
```
