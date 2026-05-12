---
tags: ["bash", "network", "cron", "curl", "schedule"]
---
# Schedule a URL Request with Cron

Sends an HTTP request to a URL on a recurring schedule using `curl` and crontab. Useful for triggering webhooks, performing periodic health checks, or keeping idle services running.

## 🛠️ How it works under the hood

1. **`cron` daemon**: A standard background UNIX service that reads predefined time patterns from text configurations and executes specific processes when the system clock matches the configuration limit.
2. **`curl` piping**: Pushing curl logs to `/dev/null` suppresses local output, while `2>&1` ensures error streams follow the suppression route, preventing the cron daemon from filling the host mailbox with request logs.

---

## 🚀 Usage Guide

### 1. Open Configuration Editor
Access the local user cron table definitions.
```bash
crontab -e
```

### 2. Add Network Handlers
Define the timeframe layout and execution target.

```bash
# Execute at minute 0 every hour
0 * * * * curl -s "https://example.com/ping" > /dev/null 2>&1

# Alternative shorthand for hourly execution
@hourly curl -s "https://example.com/ping" > /dev/null 2>&1

# Execute every 30 minutes
*/30 * * * * curl -s "https://example.com/ping" > /dev/null 2>&1

# Execute once daily exactly at 8:00 AM
0 8 * * * curl -s "https://example.com/ping" > /dev/null 2>&1
```

### 3. Verify Configurations
List stored background tasks attached to the current user configuration bounds.
```bash
crontab -l
```

---

## Technical Mapping Reference
Cron interprets five field intervals followed by the command string.
```text
┌─ minute   (0-59)
│ ┌─ hour   (0-23)
│ │ ┌─ day  (1-31)
│ │ │ ┌─ month (1-12)
│ │ │ │ ┌─ weekday (0-7, 0 and 7 = Sunday)
│ │ │ │ │
* * * * *  command
```
