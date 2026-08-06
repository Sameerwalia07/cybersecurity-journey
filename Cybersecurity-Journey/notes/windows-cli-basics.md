# Windows CLI Basics — cmd + PowerShell Reference

A running cheat sheet for Windows command line (cmd) and PowerShell,
covering both basic navigation and security-relevant commands.

## cmd — Basic Navigation

```cmd
cd                   :: show current directory
cd \path               :: change directory
dir                      :: list files/folders
dir /a                    :: list including hidden files
cls                         :: clear the screen
```

## cmd — System Info

```cmd
whoami                :: current user
ipconfig                 :: view network configuration
ipconfig /all              :: detailed network config
tasklist                     :: list running processes
taskkill /PID 1234 /F           :: force-kill a process by PID
systeminfo                        :: detailed system info
```

## PowerShell — Basics

PowerShell commands are called **cmdlets**, using a Verb-Noun format
(e.g. `Get-Process`).

```powershell
Get-Process                          # list running processes
Get-Service                            # list services
Get-ChildItem                            # list files/folders (like ls/dir)
Get-Content file.txt                       # print file contents (like cat)
Get-Location                                 # current directory (like pwd)
```

## PowerShell — Filtering & Piping

```powershell
Get-Process | Where-Object {$_.CPU -gt 50}     # processes using >50% CPU
Get-Process | Sort-Object CPU -Descending        # sort processes by CPU
Get-EventLog -LogName Security -Newest 10          # last 10 security log entries
```

## PowerShell — Security-Relevant Commands

```powershell
Get-LocalUser                       # list local user accounts
Get-NetTCPConnection                  # view active network connections
Get-ScheduledTask                       # list scheduled tasks (persistence check)
Get-WmiObject win32_startupcommand        # list startup programs
```

## Windows Event IDs to Remember (Security Log)

| Event ID | Meaning |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4688 | New process created |
| 4720 | New user account created |
| 4104 | PowerShell script block logged |
| 104  | Event log cleared (anti-forensics red flag) |

## Quick Examples

```powershell
# Find all failed logon attempts in Security log
Get-EventLog -LogName Security | Where-Object {$_.EventID -eq 4625}

# List all processes with their command line (useful for spotting
# suspicious PowerShell/cmd execution chains)
Get-CimInstance Win32_Process | Select-Object Name, CommandLine
```

---
*Windows Event IDs table is worth memorising — they come up constantly in
SIEM detection rules (see `detection-rules-cheatsheet.md`).*
