# Detection Rules Cheat Sheet — Snort + SIEM Rules

Templates and worked examples for building detection rules, pulled from
IDS Fundamentals and Introduction to SIEM.

## Snort Rule Format

```
action protocol src_ip src_port -> dst_ip dst_port (options)
```

| Component | Meaning |
|---|---|
| Action | `alert`, `log`, `pass` |
| Protocol | `tcp`, `udp`, `icmp` |
| Source IP/Port | Where traffic originates |
| Destination IP/Port | Where traffic is headed |
| msg | Human-readable description |
| sid | Unique signature ID |
| rev | Rule revision number |

**Worked example — SSH brute force detection:**
```
alert tcp any any -> 192.168.1.10 22 (msg:"Possible SSH brute force attempt"; sid:1000001; rev:1;)
```

**Template to reuse:**
```
alert <protocol> <src_ip> <src_port> -> <dst_ip> <dst_port> (msg:"<description>"; sid:<unique_id>; rev:1;)
```

## SIEM Detection Rule Logic

General pattern: **Log Source + Event ID + Specific Field/Value → Alert**

**Worked example 1 — Log clearing (anti-forensics):**
```
IF Log Source = WinEventLog AND EventID = 104
THEN Trigger alert "Event Log Cleared"
```

**Worked example 2 — Recon command detection:**
```
IF Log Source = WinEventLog AND EventCode = 4688 AND NewProcessName contains "whoami"
THEN Trigger alert "WHOAMI command Execution DETECTED"
```

**Template to reuse:**
```
IF Log Source = <source> AND EventID/Code = <id> [AND <field> contains <value>]
THEN Trigger alert "<description>"
```

## Common Windows Event IDs for Detection Rules

| Event ID | Use Case |
|---|---|
| 4624 | Successful logon (baseline / anomaly detection) |
| 4625 | Failed logon (brute force detection) |
| 4688 | Process execution (recon/malicious tool detection) |
| 4720 | New user created (privilege/persistence detection) |
| 104  | Event log cleared (anti-forensics detection) |
| 4104 | PowerShell script block (obfuscated script detection) |

## Ideas for Rules to Practice Writing

- Multiple failed logins from the same IP within 5 minutes (brute force)
- A Word/Excel process spawning PowerShell or cmd (macro-based attack)
- A new scheduled task created shortly after a suspicious login
  (persistence)
- Outbound traffic to a known-bad IP from an internal host (C2 beaconing)

---
*Good habit: whenever a new detection idea comes up in a room, draft it
here using the templates above before moving on — it's much faster to
build real fluency this way than only reading examples.*
