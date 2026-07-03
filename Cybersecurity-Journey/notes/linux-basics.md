# Linux Basics — Notes

Standalone notes that aren't tied to one specific TryHackMe room — things I've
picked up across multiple rooms/paths and want in one reference place.

## Navigating the filesystem

```bash
pwd          # print working directory
ls -la       # list all files, including hidden, with details
cd /path     # change directory
cat file     # print file contents
```

## Useful for security work specifically

```bash
whoami                  # current user
sudo -l                 # what commands can I run as sudo?
ps aux                  # running processes
netstat -tulpn          # listening ports and services
find / -perm -4000      # find SUID binaries (privilege escalation checks)
```

## Things I keep forgetting (so I'm writing them down)

- `chmod 755` = owner: read/write/execute, group & others: read/execute
- `grep -r "text" .` searches recursively in current directory
- `|` pipes output from one command into another (e.g. `cat file | grep error`)

---

*This file grows over time — update it whenever a new Linux command clicks for you.*
