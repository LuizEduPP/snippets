---
tags: ["windows", "user", "password", "cmd", "admin"]
---
# Change User Password (Windows CMD)

Changes a local Windows account password using the built-in `net user` command without needing the current password. Requires Administrator access.

## 🛠️ How it works under the hood

1. **`net user`**: A Windows built-in command that manages local user accounts — listing, creating, modifying, and deleting them through the Windows SAM (Security Account Manager) database.
2. **`net user USERNAME NEWPASSWORD`**: Bypasses the old password requirement because the SAM API allows Administrators to overwrite credentials directly, which is how it differs from standard user password changes.
3. **Admin privilege requirement**: CMD must be started with elevated rights because the SAM database is protected. Without elevation, `net user` returns "System error 5" (Access Denied).

---

## 🚀 Usage Guide

### 1. Open CMD as Administrator
Press `Win + S`, type `cmd`, right-click the result, and select **Run as administrator**.

### 2. List all local accounts
Shows every local user account and its status (Active, Disabled).
```cmd
net user
```

### 3. Change the password
Replace `USERNAME` with the exact account name shown in step 2.
```cmd
net user USERNAME NEWPASSWORD
```

**Example:**
```cmd
net user John NewPass2025!
```

A successful change prints: `The command completed successfully.`

> Note: This only works for **local accounts**. Microsoft accounts (linked to an email) must be changed through `Settings > Accounts`.
