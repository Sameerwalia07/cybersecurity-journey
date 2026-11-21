# MITRE ATT&CK Reference — Techniques Encountered So Far

A running list of MITRE ATT&CK Tactics and Techniques actually encountered
across rooms so far, instead of searching the site fresh each time.
Add new IDs here as they come up.

## Tactics (the "why") Encountered So Far

| Tactic ID | Name | Encountered In |
|---|---|---|
| TA0043 | Reconnaissance | Unified Kill Chain, Detecting Web Shells |
| TA0001 | Initial Access | Unified Kill Chain |
| TA0002 | Execution | Unified Kill Chain, MITRE ATT&CK room |
| TA0003 | Persistence | Unified Kill Chain |
| TA0004 | Privilege Escalation | Unified Kill Chain, Detecting Web Shells |
| TA0005 | Defense Evasion | Unified Kill Chain |
| TA0006 | Credential Access | Unified Kill Chain |
| TA0007 | Discovery | Unified Kill Chain |
| TA0008 | Lateral Movement | Unified Kill Chain, Detecting Web Shells |
| TA0009 | Collection | Unified Kill Chain |
| TA0010 | Exfiltration | Unified Kill Chain, Data Exfiltration Detection, Detecting Web Shells |
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
| T1110 | Brute Force | Logs Fundamentals (SPL example), Detecting Web Attacks |
| T1190 | Exploit Public-Facing Application | Detecting Web Shells (room link), Detecting Web Attacks (SQLi) |
| T1505.003 | Server Software Component: Web Shell | Detecting Web Shells (room link) |

## Module 7 & 8 Mappings (my own, verify on attack.mitre.org)

The rooms only linked a few IDs directly (T1190, T1505.003, and the tactics
above). The rest below are **my own mapping of the behaviours the rooms
described**, from memory. **Check each one on attack.mitre.org before quoting it
in a report or interview.**

### Network monitoring (Module 7)

| Technique ID | Name | Behaviour from the rooms |
|---|---|---|
| T1595 | Active Scanning | Nmap scans against the network |
| T1046 | Network Service Discovery | Port scans, service enumeration |
| T1018 | Remote System Discovery | Horizontal sweeps for live hosts |
| T1557 | Adversary-in-the-Middle | MITM attacks in general |
| T1557.002 | Adversary-in-the-Middle: ARP Cache Poisoning | ARP spoofing |
| T1040 | Network Sniffing | Packet sniffing |
| T1048 | Exfiltration Over Alternative Protocol | Exfil over DNS, FTP, ICMP |
| T1071.004 | Application Layer Protocol: DNS | DNS tunnelling / C2 over DNS |
| T1567 | Exfiltration Over Web Service | Uploads to cloud storage, webmail |
| T1560 | Archive Collected Data | Staging: zip/rar/7z before exfil |

### Web security (Module 8)

| Technique ID | Name | Behaviour from the rooms |
|---|---|---|
| T1190 | Exploit Public-Facing Application | File upload flaws, SQLi, command injection |
| T1505.003 | Server Software Component: Web Shell | `shell.php`, `.aspx` shells (Hafnium, Conti) |
| T1110 | Brute Force | Repeated `POST /login` |
| T1595.002 | Active Scanning: Vulnerability Scanning | Directory fuzzing, sqlmap/wpscan User-Agents |
| T1499 | Endpoint Denial of Service | Application-layer DoS/DDoS |
| T1499.002 | Service Exhaustion Flood | HTTP flood, Slowloris |

### Groups and software named in the rooms

| ID | Name | Where |
|---|---|---|
| G0125 | HAFNIUM | Detecting Web Shells (ProxyLogon, Exchange) |
| S0575 | Conti | Detecting Web Shells (Exchange `aspnet_client`) |

*Not every attack has a clean ATT&CK mapping: XSS, CSRF and clickjacking are
client-side and don't map neatly to one technique.*

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
