# TryHackMe — Operating System Security

**Path:** Pre Security
**Date completed:** [17/05/2026]
**Room link:** [https://tryhackme.com/room/operatingsystemsecurity]

---

## 🎯 What I Learned

- What computer hardware actually is, and why an OS is needed to make it usable
- The role of the OS as the layer between hardware and applications
- Common OS types across devices (Windows, macOS, Android, iOS)
- How the CIA Triad applies specifically at the OS level
- Common OS-level security weaknesses: weak passwords, weak file permissions,
  and exposure to malicious files

## 🧠 In My Own Words

**Computer hardware** is the physical, touchable parts of a system — the
screen, keyboard, mouse, USB storage, and the desktop board itself, which
houses the **CPU** and **RAM (memory chips)**. The desktop board also
connects to storage like an **HDD or SSD**. On their own, none of this
hardware can be used directly to actually get anything done.

This is where the **operating system (OS)** comes in. The OS sits as a layer
**between the hardware and the applications/programs** we actually use. It
controls and drives the hardware, and it decides the rules under which
applications are allowed to access and use that hardware. Without an OS,
software would have no consistent way to talk to the physical components
underneath it.

Different devices run different OS types:
- **Laptops/desktops:** Windows, macOS
- **Smartphones:** Android, iOS

**Security at the OS level comes back to the CIA Triad** — Confidentiality,
Integrity, and Availability must be ensured at this layer, since the OS is
the foundation everything else (apps, data, network access) depends on. If
the OS itself is compromised, every application running on top of it is at
risk too.

Common OS-level security weaknesses covered:
- **Weak passwords / authentication:** the National Cyber Security Centre
  has published a list of the most commonly used **100,000 passwords** —
  attackers can exploit weak, predictable passwords through methods like
  brute-forcing or credential stuffing
- **Weak file permissions:** if permissions on files/folders are set too
  loosely, users or programs can access or modify things they shouldn't be
  able to
- **Access to malicious files:** if the OS/user doesn't properly restrict or
  scan what can be opened/executed, malicious files can run and compromise
  the system

## 🛠️ Key Terms Introduced

- Hardware vs Operating System vs Applications (the three layers)
- CIA Triad applied at OS level
- Weak passwords / common password lists
- File permissions
- Malicious file exposure

## ❓ Questions I Had / Things to Revisit

- Want to look at actual file permission structures in Linux (`rwx`,
  numeric values like `755`) since I've seen the commands but want to
  connect them to this "weak permissions" security risk directly
- Curious what tools/techniques attackers actually use to exploit weak
  passwords in practice (this feels like a bridge into later offensive
  security concepts, useful to understand from a defender's perspective)
- Want to find and look through the NCSC common password list mentioned in
  this room, just to see real examples

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
the hardware-OS-application relationship and the three OS-level security
weaknesses confidently.

---

*This connects directly to Linux CLI Basics — commands like `ls -l` showing
file permissions now have real security context: those permission bits
aren't just syntax to memorise, they're literally one of the weaknesses
attackers look for.*
