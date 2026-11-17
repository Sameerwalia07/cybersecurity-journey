# Detection Rules Cheat Sheet — Snort + SIEM Rules

Templates and worked examples for building detection rules, pulled from
IDS Fundamentals, Snort, Introduction to SIEM and the Module 7 detection rooms.

## Snort Rule Format

```
action protocol src_ip src_port -> dst_ip dst_port (options)
```

| Component | Meaning |
|---|---|
| Action | `alert`, `log`, `pass`, `drop`, `reject` (see below) |
| Protocol | `tcp`, `udp`, `icmp`, `ip` (Snort 2 supports only these four) |
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

### Snort actions

| Action | Effect |
|---|---|
| `alert` | Alert and log (IDS) |
| `log` | Log only |
| `drop` | Block and log (IPS) |
| `reject` | Block, log and terminate the session (IPS) |

Snort is **passive (IDS) by default**. IPS needs inline mode (`-Q --daq afpacket`).

### Direction, IP and port patterns

| Want | Write |
|---|---|
| Source to destination only | `->` |
| Both directions | `<>` (there is **no** `<-`) |
| One IP / a subnet | `192.168.1.56` / `192.168.1.0/24` |
| Several ranges | `[192.168.1.0/24, 10.1.1.0/24]` |
| Everything except | `!192.168.1.0/24` |
| Port range 1-1024 | `1:1024` |
| Up to 1024 / 1025 and above | `:1024` / `1025:` |
| Specific ports | `[21,23]` |
| Not port 21 | `!21` |

Snort 2 has no `ftp`/`http` protocol keyword. Use TCP plus the port
(FTP = `tcp` port 21).

### Rule options

| Option | What it does |
|---|---|
| `msg` | Alert text |
| `sid` | Unique ID: `<100` reserved, `100-999,999` shipped rules, **`>=1,000,000` mine** |
| `rev` | Revision number (I keep my own history) |
| `reference` | CVE or external link, e.g. `reference:cve,CVE-XXXX;` |
| `content` | Payload match, ASCII or HEX (`"GET"` = `"\|47 45 54\|"`), case-sensitive |
| `nocase` | Ignore case for the content match |
| `fast_pattern` | Which content is checked first; required with multiple `content` options, once per rule |
| `flags` | TCP flags: `F` FIN, `S` SYN, `R` RST, `P` PSH, `A` ACK, `U` URG |
| `dsize` | Payload size: `dsize:>100`, `dsize:<100`, `dsize:100<>300` |
| `id` | IP ID field |
| `sameip` | Source and destination IP are identical |

### More worked Snort examples

```
# ICMP / ping sweep visibility
alert icmp any any -> $HOME_NET any (msg:"ICMP Packet Found"; sid:1000002; rev:1;)

# SYN packets (basic scan visibility, pair with a threshold in real use)
alert tcp any any -> $HOME_NET any (msg:"TCP SYN Detected"; flags:S; sid:1000003; rev:1;)

# HTTP GET requests (case-insensitive)
alert tcp any any -> any 80 (msg:"HTTP GET Request"; content:"GET"; nocase; sid:1000004; rev:1;)

# Any FTP command channel activity
alert tcp any any <> any 21 (msg:"FTP Port 21 Activity Detected"; sid:1000005; rev:1;)

# Large payloads (possible data leaving, tune the size to my environment)
alert tcp $HOME_NET any -> $EXTERNAL_NET any (msg:"Large Outbound Payload"; dsize:>1000; sid:1000006; rev:1;)
```

*These are practice rules. Real deployments need thresholds so one scan
does not create thousands of alerts.*

### Snort command cheat sheet

| Goal | Command |
|---|---|
| Version | `snort -V` |
| Test config | `sudo snort -c /etc/snort/snort.conf -T` |
| Sniff (headers / payload / link layer / full hex) | `sudo snort -v` / `-d` / `-e` / `-X` (combine: `-dev`) |
| Pick an interface | `sudo snort -v -i eth0` |
| Log to current dir | `sudo snort -dev -l .` |
| Log in ASCII | `sudo snort -dev -K ASCII` |
| Read a log, filter with BPF | `sudo snort -r file.log 'udp and port 53'` |
| Process only N packets | `snort -dvr file.log -n 10` |
| IDS mode, console alerts | `sudo snort -c /etc/snort/snort.conf -A console` |
| IDS mode, no banner | add `-q` |
| Disable logging / run in background | `-N` / `-D` |
| IPS (inline) mode | `-Q --daq afpacket -i eth0:eth1` |
| Run on a pcap with rules | `sudo snort -c /etc/snort/snort.conf -q -r file.pcap -A console` |
| Several pcaps, show names | `--pcap-list="a.pcap b.pcap" --pcap-show` |

**Alert modes (`-A`):** `console` (fast style on screen), `cmg` (headers +
payload, hex and text), `fast` (file, no console), `full` (file, default,
no console), `none` (no alert file; traffic still logged).

**Log files are owned by root** when run with `sudo`: read them with `sudo`
or `sudo chown <user> -R <dir>`.

### Key Snort files

- `snort.conf`: main config (`HOME_NET`, `EXTERNAL_NET`, `RULE_PATH`, DAQ/IPS
  settings, output plugins, `include $RULE_PATH/local.rules`)
- `local.rules`: my own rules. `#` comments a line out; remove it to activate.
- In Snort 3 the config is `snort.lua` and its location varies.

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

## Detection Ideas from Module 7 (Network Security Monitoring)

| Threat | What to look for | Where |
|---|---|---|
| **Port scan (vertical)** | One source, many destination **ports** on one host; lots of SYN with no completed handshake | Firewall logs, Wireshark `tcp.flags.syn==1 && tcp.flags.ack==0`, Snort `flags:S` + threshold |
| **Host sweep (horizontal)** | One source, one port, many destination **hosts** | Firewall/NetFlow |
| **ARP spoofing** | Two MACs claiming one IP (especially the gateway), gratuitous ARP replies, high ARP volume | Wireshark `arp.duplicate-address-detected`, `arp.isgratuitous` |
| **DNS spoofing** | Multiple responses to one query, response from unexpected IP, very short TTL | Wireshark `dns`, DNS logs |
| **SSL stripping** | 443 request then port-80 traffic for the same domain; redirects to HTTP; cert errors | Proxy/Wireshark `http` |
| **Exfil over HTTP/S** | Large or frequent POSTs, uploads to cloud storage or webmail | Proxy logs |
| **Exfil over DNS** | Long, high-entropy hostnames, many TXT queries to one domain | DNS logs |
| **Exfil over FTP/ICMP** | Large `STOR` transfers, oversized ICMP payloads (`dsize`) | Firewall, Snort |
| **Staging before exfil** | Archive creation (zip/rar/7z) then outbound connection | Sysmon/EDR (Event IDs 1, 3, 11) |

## Ideas for Rules to Practice Writing

- Multiple failed logins from the same IP within 5 minutes (brute force)
- A Word/Excel process spawning PowerShell or cmd (macro-based attack)
- A new scheduled task created shortly after a suspicious login
  (persistence)
- Outbound traffic to a known-bad IP from an internal host (C2 beaconing)
- A Snort rule for a SYN scan with a threshold
- A SIEM rule for a large outbound upload followed by archive creation on the same host
- Alert when one IP has two ARP replies with different MACs

---
*Good habit: whenever a new detection idea comes up in a room, draft it
here using the templates above before moving on — it's much faster to
build real fluency this way than only reading examples.*
