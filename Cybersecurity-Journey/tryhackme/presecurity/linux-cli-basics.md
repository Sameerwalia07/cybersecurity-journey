# TryHackMe — Linux CLI Basics

**Path:** Pre Security
**Date completed:** [16/05/2026]
**Room link:** [https://tryhackme.com/room/linuxclibasics]

---

## 🎯 What I Learned

- What a terminal is and why it's used over a GUI in security work
- Core navigation and file-listing commands
- How to check disk usage and explore key system directories

## 🧠 In My Own Words

The **terminal** is a text-based interface for controlling a Linux system —
instead of clicking through menus and folders like in a GUI, you type
commands directly. It's faster once you're comfortable with it, and a huge
number of security tools are built to run in the terminal rather than as
graphical apps, so this is a skill that's non-negotiable for security work.

**Commands covered:**

- `pwd` — prints the current working directory (shows exactly where you are
  in the filesystem)
- `ls` — lists the files and folders in the current directory
- `ls -l` — lists them in **long format**, showing permissions, owner, size,
  and last modified date
- `ls -al` — same as `-l`, but also shows **hidden files** (files/folders
  starting with a `.`)
- `cd` — change directory, move into a specified folder
- `cd ..` — move **up one level** to the parent directory
- `cat` — print the contents of a file directly to the terminal
- `find` — search for files/directories matching a given name or pattern
  across the filesystem
- `df -h` — shows disk space usage in a **human-readable** format (GB/MB
  instead of raw bytes)
- `/etc` — an important system directory that holds configuration files for
  the system and installed programs

## 🛠️ Key Terms / Commands Introduced

```bash
pwd
ls
ls -l
ls -al
cd
cd ..
cat
find
df -h
```

## ❓ Questions I Had / Things to Revisit

- Want to go deeper into what specifically lives inside `/etc` and which
  files there matter most for security work (e.g. `/etc/passwd`,
  `/etc/shadow`)
- Want more practice combining `find` with different flags/options for more
  targeted searches
- Curious about piping commands together (`|`) to chain them — haven't
  covered this yet but know it's coming

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I'm
comfortable with these core commands and what each one does.

---

*This is the start of what I expect to be a running reference — I'll keep
adding new commands to `notes/linux-basics.md` as I pick them up across
future rooms, since Linux comfort is foundational for basically all SOC and
security tooling.*
