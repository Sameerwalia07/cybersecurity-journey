# Networking Tools — Nmap, Wireshark, Tcpdump, NetworkMiner Reference

A practical syntax cheat sheet for network/traffic analysis tools covered
across Cyber Security 101 and SOC Level 1.

## Nmap — Network Scanning

```bash
nmap 192.168.1.1                    # basic scan of a single host
nmap 192.168.1.0/24                   # scan an entire subnet
nmap -sV 192.168.1.1                    # detect service versions
nmap -sC 192.168.1.1                      # run default scripts
nmap -p 1-1000 192.168.1.1                  # scan a specific port range
nmap -p- 192.168.1.1                          # scan all 65535 ports
nmap -O 192.168.1.1                             # attempt OS detection
nmap -A 192.168.1.1                               # aggressive scan (OS, version, scripts, traceroute)
nmap -sT 192.168.1.1                                # TCP Connect scan (non-privileged)
nmap -sS 192.168.1.1                                  # SYN scan (privileged, stealthier)
nmap -sU 192.168.1.1                                    # UDP scan
```

### Recognising Nmap Scans in Wireshark (by TCP flags)

| Scan Type | Command | Handshake Behavior | Typical Window Size |
|---|---|---|---|
| TCP Connect | `-sT` | Completes full 3-way handshake | >1024 bytes |
| SYN Scan | `-sS` | Sends RST after SYN-ACK (never completes) | <=1024 bytes |
| UDP Scan | `-sU` | No handshake; closed ports get ICMP Type 3 Code 3 | -- |

```
tcp.flags.syn == 1                          # SYN packets
tcp.flags.ack == 1                            # ACK packets
(tcp.flags.syn==1) and (tcp.flags.ack==1)       # SYN-ACK
tcp.flags.reset == 1                              # RST packets
tcp.flags.fin == 1                                  # FIN packets
```

---

## Wireshark — Display Filters

### Basic Filters
```
ip.addr == 192.168.1.1              # traffic to/from a specific IP (either direction)
ip.src == 192.168.1.1                 # traffic FROM this IP only
ip.dst == 192.168.1.1                   # traffic TO this IP only
ip.addr == 10.10.10.0/24                  # subnet match
tcp.port == 443                             # traffic on a specific port
udp.port == 53
http.request                                  # only HTTP requests
http.response.code == 200                       # specific HTTP status
http.request.method == "POST"                     # only POST requests
dns                                                 # only DNS traffic
```

### Comparison Operators
| English | Symbol | Example |
|---|---|---|
| eq | == | ip.src == 10.10.10.100 |
| ne | != | avoid, use !(value) instead for reliability |
| gt | > | ip.ttl > 250 |
| lt | < | ip.ttl < 10 |
| ge | >= | ip.ttl >= 0xFA |
| le | <= | ip.ttl <= 0xA |

### Logical Operators
```
(ip.src==A) and (ip.src==B)     # AND
(ip.src==A) or (ip.src==B)        # OR
!(ip.src == 10.10.10.222)           # NOT (preferred over !=)
```

### Advanced Filter Functions
```
http.server contains "Apache"                   # substring search (case-sensitive)
http.host matches "\.(php|html)"                  # regex match (case-insensitive)
tcp.port in {80 443 8080}                           # set membership
upper(http.server) contains "APACHE"                  # case conversion before match
lower(http.server) contains "apache"
string(frame.number) matches "[13579]$"                 # convert non-string to string for matching
```

### Protocol-Specific Filters

**HTTP:**
```
http.user_agent contains "nmap"                       # scanner detection
http.request.uri contains "admin"                        # path probing
http.server contains "apache"                               # server fingerprint
(http.user_agent contains "sqlmap") or (http.user_agent contains "Nikto")  # audit tool detection
```

**ARP (MITM/poisoning detection):**
```
arp                                          # all ARP traffic
arp.opcode == 1                                # ARP requests
arp.opcode == 2                                  # ARP responses
arp.dst.hw_mac==00:00:00:00:00:00                  # ARP scanning
arp.duplicate-address-detected                       # possible poisoning
```

**DHCP:**
```
dhcp or bootp                            # all DHCP traffic
dhcp.option.dhcp == 3                      # DHCP Request (has hostname)
dhcp.option.dhcp == 5                        # DHCP ACK
dhcp.option.dhcp == 6                          # DHCP NAK
dhcp.option.hostname contains "keyword"          # hostname search
```

**NBNS / Kerberos (host & user identification):**
```
nbns.name contains "keyword"                                        # NetBIOS name search
kerberos.CNameString contains "keyword"                                # username search
kerberos.CNameString and !(kerberos.CNameString contains "$")           # exclude hostnames
```

**Tunneling detection (ICMP/DNS):**
```
data.len > 64 and icmp          # oversized ICMP payload (tunneling sign)
dns and !mdns                     # DNS traffic, excluding local link noise
```

**FTP (cleartext credential hunting):**
```
ftp.response.code == 230                                           # login success
ftp.response.code == 530                                             # login failed (brute-force signal)
ftp.request.command == "USER"
ftp.request.command == "PASS"
(ftp.request.command=="PASS") and (ftp.request.arg=="password")          # password spray signal
```

**HTTPS/TLS:**
```
tls.handshake.type == 1        # Client Hello
tls.handshake.type == 2          # Server Hello
```

### Useful Right-Click Actions
- **Apply as Filter** -- instantly filter by a clicked field's value
- **Prepare as Filter** -- builds the query without executing (for combining with AND/OR)
- **Conversation Filter** -- show only packets in a full IP+port conversation
- **Colourise Conversation** -- highlight linked packets without filtering the view
- **Apply as Column** -- add a field as its own visible column
- **Follow -> TCP/UDP/HTTP Stream** -- reconstruct a full conversation

### Useful Built-In Tools
- **Statistics -> Protocol Hierarchy** -- protocol breakdown by count/%
- **Statistics -> Conversations / Endpoints** -- traffic pairs vs unique values
- **Statistics -> DNS / HTTP** -- protocol-specific breakdowns
- **Tools -> Credentials** -- auto-extracts cleartext creds (FTP, HTTP, IMAP, POP, SMTP)
- **Tools -> Firewall ACL Rules** -- generates ready-to-use firewall rules (iptables, Cisco IOS, pf, Windows Firewall, etc.)
- **File -> Export Objects** -- extracts transferred files (DICOM, HTTP, IMF, SMB, TFTP)

---

## Tcpdump — Command-Line Packet Capture

```bash
tcpdump -i eth0                       # capture on interface eth0
tcpdump -i eth0 port 80                 # capture only port 80 traffic
tcpdump -i eth0 host 192.168.1.1          # capture traffic to/from an IP
tcpdump -i eth0 -w capture.pcap             # write capture to a file
tcpdump -r capture.pcap                       # read a saved capture file
tcpdump -i eth0 -c 100                          # capture only 100 packets
```

---

## NetworkMiner — Quick Overview Tool

Use **before** Wireshark for a fast first pass on a PCAP -- pulls out hosts,
files, credentials, and keywords automatically without manual filtering.

| Tab | What It Shows |
|---|---|
| Hosts | IP, MAC, OS (via Satori/p0f), open ports, sessions |
| Sessions | Client/server pairs, ports, protocol, start time |
| DNS | Queries, TTL, transaction ID/type |
| Credentials | Kerberos/NTLM hashes, RDP/HTTP cookies, FTP/SMTP/IMAP creds |
| Files | Extracted files with reconstructed path |
| Images | Extracted images, viewable directly |
| Parameters | Extracted form/URL parameters |
| Keywords | Custom keyword search across all capture data (reload case files after changing keywords!) |
| Messages | Extracted emails/chats |
| Anomalies | Built-in detections (e.g. EternalBlue, spoofing) -- not a full IDS |

**Workflow:** capture traffic -> **NetworkMiner** for quick overview/low-hanging fruit -> **Wireshark** for deep packet-level investigation.

---

## Quick Tool Comparison

| Tool | Best For |
|---|---|
| **Nmap** | Discovering hosts/services/open ports on a network |
| **Wireshark** | Deep, filterable, packet-by-packet analysis (GUI) |
| **Tcpdump** | Quick packet capture on servers without a GUI |
| **NetworkMiner** | Fast overview, file/credential extraction, host fingerprinting |

---
*Update this file whenever a new filter or tool trick comes up in future
rooms -- this is meant to be the fastest place to check syntax mid-investigation.*
