---
tags: ["shell-windows", "user", "password"]
---
# Change User Password (Windows CMD)

Lists local users and changes a password without needing the current one. Run CMD as Administrator.

## Command

### List local users

```cmd
net user
```

### Change password

```cmd
net user USERNAME NEWPASSWORD
```

**Example:**
```cmd
net user John NewSecurePass123
```

> `net user` requires Administrator privileges. Open CMD with `Win + S` → type `cmd` → right-click → *Run as administrator*.
