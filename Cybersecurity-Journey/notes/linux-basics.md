# Linux Basics — Command Reference

A running cheat sheet of Linux commands picked up across multiple rooms
and paths. Updated as new commands are learned — not tied to one room.

## Navigation

```bash
pwd                    # print working directory
ls                     # list files/folders
ls -l                  # long format (permissions, owner, size, date)
ls -al                 # long format + hidden files
cd /path               # change directory
cd ..                  # move up one level
```

## Viewing Files

```bash
cat file               # print full file contents
less file               # view file page by page (Space = next, b = back)
head file               # view first 10 lines
tail file                # view last 10 lines
tail -f file              # follow a file live (great for watching logs)
```

## Searching

```bash
grep "text" file            # search for "text" in a file
grep -r "text" .             # recursive search in current directory
grep -i "text" file           # case-insensitive search
grep -c "text" file            # count matching lines
find / -name "filename"         # find a file by name system-wide
find / -perm -4000              # find SUID binaries (priv-esc checks)
```

## File Info & Permissions

```bash
df -h                    # disk usage, human-readable
chmod 755 file             # set permissions (owner rwx, group/others rx)
chmod +x file                # make a file executable
chown user:group file          # change file owner/group
```

## System / Process Info

```bash
whoami                    # current user
sudo -l                     # what can I run as sudo?
ps aux                       # list running processes
kill -9 PID                    # force-kill a process by PID
top                              # live process/resource monitor
```

## Log Locations (security-relevant)

```
/etc/passwd            # user account info
/etc/shadow             # hashed passwords (root-readable only)
/var/log/auth.log        # authentication logs (Debian/Ubuntu)
/var/log/secure           # authentication logs (RHEL/CentOS)
/var/log/httpd             # Apache/HTTP request & error logs
/var/log/cron                # scheduled job logs
/var/log/kern                 # kernel events
```

## Piping & Redirection

```bash
command1 | command2       # pipe output of command1 into command2
command > file              # overwrite file with command output
command >> file               # append command output to file
```

## Quick Examples

```bash
# Search auth logs for failed SSH logins
grep "Failed password" /var/log/auth.log

# Find all files modified in the last 1 day
find / -mtime -1

# Show top 10 largest files in current directory
du -ah . | sort -rh | head -10
```

---
*Add to this file any time a new command clicks in a room — the goal is
one place to check instead of hunting back through old writeups.*
