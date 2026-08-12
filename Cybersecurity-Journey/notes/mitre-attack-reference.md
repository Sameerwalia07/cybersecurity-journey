# MITRE ATT&CK Reference — Techniques Encountered So Far

A running list of MITRE ATT&CK Tactics and Techniques actually encountered
across rooms so far, instead of searching the site fresh each time.
Add new IDs here as they come up.

## Tactics (the "why") Encountered So Far

| Tactic ID | Name | Encountered In |
|---|---|---|
| TA0043 | Reconnaissance | Unified Kill Chain |
| TA0001 | Initial Access | Unified Kill Chain |
| TA0002 | Execution | Unified Kill Chain, MITRE ATT&CK room |
| TA0003 | Persistence | Unified Kill Chain |
| TA0004 | Privilege Escalation | Unified Kill Chain |
| TA0005 | Defense Evasion | Unified Kill Chain |
| TA0006 | Credential Access | Unified Kill Chain |
| TA0007 | Discovery | Unified Kill Chain |
| TA0008 | Lateral Movement | Unified Kill Chain |
| TA0009 | Collection | Unified Kill Chain |
| TA0010 | Exfiltration | Unified Kill Chain |
| TA0011 | Command and Control | Unified Kill Chain |
| TA0040 | Impact | Unified Kill Chain |

## Techniques (the "how") Encountered So Far

| Technique ID | Name | Encountered In |
|---|---|---|
| T1566 | Phishing | MITRE ATT&CK room (threat intel example) |
| T1059.001 | Command and Scripting Interpreter: PowerShell | MITRE ATT&CK room |
| T1003.001 | OS Credential Dumping: LSASS Memory | MITRE ATT&CK room |
| T1021.002 | Remote Services: SMB/Windows Admin Shares | MITRE ATT&CK room |
| T1543.003 | Create or Modify System Process: Windows Service | Cyber Kill Chain (Installation phase) |
| T1070.006 | Indicator Removal: Timestomping | Cyber Kill Chain (Installation phase) |
| T1078 | Valid Accounts | MITRE ATT&CK room (D3FEND example) |
| T1110 | Brute Force | Logs Fundamentals (SPL example) |

## D3FEND Defensive Techniques Encountered

| Technique ID | Name | Counters (ATT&CK) |
|---|---|---|
| D3-CRO | Credential Rotation | T1078 (Valid Accounts), T1003 (Credential Dumping) |

## D3FEND's 7 Tactics (for reference)

Model → Harden → Detect → Isolate → Deceive → Evict → Restore

## How to Use This File

When a new room mentions a MITRE technique:
1. Add it to the table above with the room it came from
2. Note what Tactic it falls under
3. If a matching D3FEND defence is mentioned, note it in the D3FEND table

Over time this becomes a genuinely useful personal ATT&CK reference,
built from what's actually been learned rather than the entire matrix at
once.

---
*Pairs with the Pyramid of Pain — TTPs (this file) are the hardest, most
valuable indicators to detect, per that framework.*
