---
tags: ["shell-linux", "vscode", "url-handler"]
---
# Register vscode:// URL Protocol Handler (Linux)

Registers the `vscode://` protocol so links like `vscode:///path/to/file.ts:10` open directly in VS Code from the browser or terminal.

Paste and run directly in the terminal — no file needed.

## Command

### Create and register the handler

```bash
cat > ~/.local/share/applications/vscode-url-handler.desktop << 'EOF'
[Desktop Entry]
Name=VS Code URL Handler
Exec=/usr/share/code/bin/code --open-url %U
Type=Application
NoDisplay=true
MimeType=x-scheme-handler/vscode;
EOF

xdg-mime default vscode-url-handler.desktop x-scheme-handler/vscode
update-desktop-database ~/.local/share/applications/
```

> For VS Code OSS or Codium, replace the `Exec` path:
> - VS Code OSS: `/usr/bin/code-oss --open-url %U`
> - Codium: `/usr/bin/codium --open-url %U`

### Test it

```bash
# Open VS Code
xdg-open "vscode://"

# Open a specific file
xdg-open "vscode:///home/user/projects/myproject/index.ts"

# Open at a specific line and column
xdg-open "vscode:///home/user/projects/myproject/index.ts:42:5"
```

---

## Windows (PowerShell)

```powershell
New-Item -Path "HKCU:\Software\Classes\vscode" -Force
Set-ItemProperty -Path "HKCU:\Software\Classes\vscode" -Name "(Default)" -Value "URL:VS Code Protocol"
Set-ItemProperty -Path "HKCU:\Software\Classes\vscode" -Name "URL Protocol" -Value ""

New-Item -Path "HKCU:\Software\Classes\vscode\shell\open\command" -Force
$codePath = (Get-Command code).Source
Set-ItemProperty -Path "HKCU:\Software\Classes\vscode\shell\open\command" -Name "(Default)" -Value "`"$codePath`" --open-url `"%1`""
```
