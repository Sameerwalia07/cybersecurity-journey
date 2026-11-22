# 📖 Glossary — SOC Level 1 (Part 2: Modules 5–8)

A one-stop revision and quick-reference file for the second half of what's
been completed in TryHackMe SOC Level 1: **Phishing Analysis, Network Traffic
Analysis, Network Security Monitoring and Web Security Monitoring.**

> 💡 **How to use:** skim a section before an interview or when a term feels
> fuzzy. **Part 1** (Modules 1–4) is in `glossary-soclevel1-part1.md`. New
> modules will be added as they are completed.

## 🔎 Quick A–Z Index

- Access Log *(Module 8)*  
- ARP Poisoning/Spoofing *(Module 6)*  
- Attack Surface *(Module 7)*  
- Capture Filter vs Display Filter *(Module 6)*  
- CDN (Content Delivery Network) *(Module 8)*  
- Client-side attacks *(Module 8)*  
- Content-Type / Content-Disposition / Content-Transfer-Encoding *(Module 5)*  
- Data Exfiltration *(Module 7)*  
- Defanging *(Module 5)*  
- Detection Techniques *(Module 7)*  
- Directory Fuzzing *(Module 8)*  
- DoS vs DDoS *(Module 8)*  
- Email Header *(Module 5)*  
- Filter functions *(Module 6)*  
- Header/URL/File Analysis Tools *(Module 5)*  
- Horizontal vs Vertical Scanning *(Module 7)*  
- IDS vs IPS *(Module 7)*  
- Input Validation and Sanitisation *(Module 8)*  
- Kerberos *(Module 6)*  
- MITM (Man-in-the-Middle) *(Module 7)*  
- NetFlow / IPFIX *(Module 6)*  
- Network Perimeter *(Module 7)*  
- Network TAP *(Module 6)*  
- NetworkMiner *(Module 6)*  
- Nmap Scan Patterns: *(Module 6)*  
- North-South traffic *(Module 6)*  
- NTA (Network Traffic Analysis) *(Module 6)*  
- Ping Sweep *(Module 7)*  
- Request–Response Cycle *(Module 8)*  
- S/MIME *(Module 5)*  
- Sandbox *(Module 5)*  
- Scanning vs Brute-forcing vs Beaconing *(Module 7)*  
- Server-side attacks *(Module 8)*  
- SMTP *(Module 5)*  
- Snort *(Module 7)*  
- Spam *(Module 5)*  
- SPF (Sender Policy Framework) *(Module 5)*  
- Statistics tools *(Module 6)*  
- Status Codes *(Module 8)*  
- TLS Handshake (Client Hello / Server Hello) *(Module 6)*  
- URL Shortening Abuse *(Module 5)*  
- Web Service Components *(Module 8)*  
- Web Shell *(Module 8)*  
- Wireshark *(Module 6)*

---

## Module 5 — Phishing Analysis

**SMTP** (sending email, port 25/587), **POP3** (downloads mail to a client), **IMAP** (syncs mail on the server) — the core email protocols.

**Email Header** — metadata showing the route and authentication of a message. Key fields: **From**, **Return-Path**, **Reply-To**, **Received** (read bottom-up for the true path), **Message-ID**, **X-Originating-IP**, **Authentication-Results**.
*Scenario: From says `ceo@company.com` but Return-Path is `bob@random-host.ru` and Reply-To differs: a spoofing sign.*

**Content-Type / Content-Disposition / Content-Transfer-Encoding** — headers describing the body, whether it is inline or an attachment, and how it is encoded (e.g. Base64).

**Spam** — unwanted bulk mail. **Malspam** — spam carrying malware. **Phishing** — fraudulent mail to steal credentials or deliver malware. **Spear Phishing** — targeted at a person. **Whaling** — targets executives. **Smishing** — by SMS. **Vishing** — by voice call.

**Defanging** — modifying links/addresses so they can't be clicked by accident: `hxxps://evil[.]com`, `user[@]domain[.]com`.

**Header/URL/File Analysis Tools** — **Messageheader / Message Header Analyzer** (parse headers), **IPinfo** (IP details), **URLScan.io** (safely load and screenshot a URL), **Talos Reputation Center** (IP/domain reputation), **VirusTotal** (multi-engine scan by file, hash, URL), `sha256sum` (get a file hash on Linux).

**Sandbox** — an isolated environment to run suspicious files safely: **ANY.RUN** (interactive), **Hybrid Analysis**, **JOESandbox**. **PhishTool** — a tool for phishing email analysis and classification.

**URL Shortening Abuse** — hiding the real destination behind a short link; **WhereGoes** expands them safely. **Tracking Pixel** — a hidden image that tells the sender when the email is opened. **Multi-stage Redirection** — a chain of hops to evade filters. **Credential Harvesting Portal** — a fake login page. **BCC Abuse** — sending to many hidden recipients. **`.dot` / `.xlsx` payloads** — Office files with macros or malicious content.

**SPF (Sender Policy Framework)** — a DNS record listing servers allowed to send for a domain. **DKIM (DomainKeys Identified Mail)** — a cryptographic signature proving the message wasn't altered and came from the domain. **DMARC** — a policy telling receivers what to do if SPF/DKIM fail (none/quarantine/reject) and requiring **alignment** with the From domain.

**S/MIME** — email **digital signatures** (authenticity/integrity) and **encryption** (confidentiality). **SEG (Secure Email Gateway)** — filters mail before delivery. **Link Rewriting** — replaces URLs with checked proxy URLs. **Sandboxing (email)** — detonating attachments before delivery.

---

## Module 6 — Network Traffic Analysis

**NTA (Network Traffic Analysis)** — inspecting network traffic to detect threats and investigate incidents.

**North-South traffic** — in and out of the network (to/from the internet). **East-West traffic** — between internal systems (where lateral movement hides).

**Network TAP** — a hardware device copying traffic for monitoring. **Port Mirroring / SPAN** — a switch copying traffic from one port to a monitoring port.

**NetFlow / IPFIX** — summaries of conversations (who talked to whom, how much) without the content. Lightweight, good for spotting volume anomalies.

**Kerberos** — Windows domain authentication using tickets: **TGT (Ticket Granting Ticket)** and **Service Ticket**, seen in SMB authentication flows.

**Wireshark** — the standard packet analyser. **Packet details layers** — Frame → Ethernet → IP → TCP/UDP → Application data. **Expert Info** — flags (Chat, Note, Warn, Error). **Export Objects** — extract files from protocols like HTTP.

**Capture Filter vs Display Filter** — a *capture filter* (BPF syntax) limits what's recorded; a *display filter* (Wireshark syntax) hides packets from view after capture. **Prepare as Filter vs Apply as Filter** — build a filter without or with applying it immediately.

**Statistics tools** — **Protocol Hierarchy** (which protocols), **Conversations** (pairs of hosts), **Endpoints** (individual hosts), **Resolved Addresses**. **Name Resolution** and **GeoIP (MaxMind)** add readable names and locations.

**Filter functions** — `contains`, `matches` (regex), `in`, `upper()`, `lower()`, `string()`.

**Nmap Scan Patterns:** **TCP Connect Scan** (full handshake), **SYN Scan** (half-open: SYN, SYN/ACK, RST), **UDP Scan** (UDP probes, ICMP port unreachable replies).

**ARP Poisoning/Spoofing** and **Gratuitous ARP** — see Module 7. **DHCP / NBNS / Kerberos** — traffic that helps identify hostnames and users. **ICMP Tunnelling / DNS Tunnelling** — data hidden in those protocols.

**TLS Handshake (Client Hello / Server Hello)** — start of an encrypted session; **SSLKEYLOGFILE** lets Wireshark decrypt TLS in a lab. Wireshark's **Credentials tool** lists captured credentials; the **Firewall ACL Rules** generator creates block rules.

**NetworkMiner** — an NFAT (**Network Forensic Analysis Tool**) that extracts hosts, files, images and credentials from PCAPs. **Satori / p0f** — OS fingerprinting engines. **mac-ages** — MAC-vendor lookup database.

---

## Module 7 — Network Security Monitoring

**Network Perimeter** — the boundary between the internal network and the internet. **DMZ (Demilitarised Zone)** — a separate zone for public-facing servers.

**Scanning vs Brute-forcing vs Beaconing** — scanning: one source, many ports/hosts; brute-forcing: many attempts at one service; beaconing: regular timed check-ins to a C2.

**Attack Surface** — everything an attacker could target. **External scanning** (Reconnaissance, TA0043) vs **Internal scanning** (Discovery, TA0007).

**Horizontal vs Vertical Scanning** — horizontal: one port across many hosts; vertical: many ports on one host.

**Ping Sweep** — ICMP to find live hosts. **TCP SYN Scan** — half-open port scan. **UDP Scan** — probing UDP ports.

**Data Exfiltration** — unauthorised transfer of data out. Channels: **DNS tunnelling** (long, high-entropy hostnames, many TXT queries; **NXDOMAIN** floods), **FTP** (`STOR`/`RETR`, **PASV** passive mode), **HTTP/S** (large POSTs, chunked/multipart uploads, **SNI** analysis), **ICMP tunnelling** (oversized echo payloads, fragmentation).
*Scenario: a workstation sends hundreds of DNS TXT queries to one odd domain with 60-character subdomains: likely DNS exfil.*

**MITM (Man-in-the-Middle)** — intercepting and possibly altering traffic between two parties. **ARP Spoofing** — forged ARP replies make the attacker's MAC the gateway's. Signs: two MACs for one IP, **gratuitous ARP**, high ARP volume. **DNS Spoofing** — forged DNS answers (multiple responses to one query, short TTL). **SSL Stripping** — downgrading HTTPS to HTTP. **Session Hijacking**, **Rogue Access Point**, **IP Spoofing** — other MITM paths.

**IDS vs IPS** — IDS *detects and alerts* (passive); IPS *detects and blocks* (inline). **HIDS** (one host) vs **NIDS** (network). **NIPS, NBA, WIPS, HIPS** — network, behaviour-based, wireless and host prevention systems.

**Detection Techniques** — **Signature-based** (known patterns), **Anomaly/behaviour-based** (deviation from a **baseline**), **Policy-based**, **Hybrid**. **Zero-day** evades signatures; anomaly methods can catch it but produce more **false positives**.

**Snort** — open-source IDS/IPS. **Modes:** sniffer (`-v`, `-d`, `-e`, `-X`), packet logger (`-l`, `-K ASCII`), NIDS/NIPS (`-c`, `-A`), PCAP mode (`-r`). **Rule format:** `action protocol src_ip src_port -> dst_ip dst_port (options)`. **Actions:** `alert`, `log`, `drop`, `reject`. **Options:** `msg`, `sid` (user rules ≥ 1,000,000), `rev`, `content`, `nocase`, `fast_pattern`, `flags`, `dsize`, `sameip`. **Files:** `snort.conf` / `snort.lua`, `local.rules`. **Variables:** `$HOME_NET`, `$EXTERNAL_NET`. **DAQ** — data acquisition modules (`pcap`, `afpacket`). **Promiscuous mode** — capturing traffic not addressed to the host.

---

## Module 8 — Web Security Monitoring

**Web Service Components** — **application**, **web server** (Apache, Nginx, IIS), **host machine**. Each needs its own protection.

**Request–Response Cycle** — browser requests, server responds. **GET** retrieves; **POST** submits data; **PUT** uploads/replaces; **DELETE** removes; **OPTIONS** lists methods; **HEAD** returns headers only.

**Access Log** — a record of every web request: client IP, timestamp, request, status code, size, referrer, User-Agent. **User-Agent** — identifies the client software (and attack tools like `sqlmap`).

**Status Codes** — `200` OK, `302` redirect (often a successful login), `404` not found (probing), `503` service unavailable (overload).

**Input Validation and Sanitisation** — checking and cleaning user input to stop injection. **Least Privilege** — giving services only the access they need. **System Hardening** — removing unnecessary services and closing ports.

**CDN (Content Delivery Network)** — edge servers cache content, mask the origin IP, absorb DDoS and often include a WAF. **WAF** — inspects HTTP traffic using signature, heuristic, behavioural and reputation rules. **Rate Limiting** — capping requests per IP/time (e.g. 5 logins/minute). **CAPTCHA / JavaScript Challenge** — bot checks.

**Client-side attacks** (happen in the browser, hard for the SOC to see): **XSS** (script runs in a victim's browser), **CSRF** (browser tricked into sending an unwanted request), **Clickjacking** (invisible overlays).

**Server-side attacks** (leave log evidence): **Brute Force**, **SQL Injection** (query built by concatenation, not **parameterised queries**), **Command Injection** (input passed to the OS).
*Scenario: `GET /search?q=' OR '1'='1` from a `sqlmap` User-Agent is an SQL injection attempt.*

**Directory Fuzzing** — requesting many paths to find hidden pages (many 404s, few 200s).

**Web Shell** — a malicious script on a web server giving remote command execution (T1190 / T1505.003). Abused PHP functions: `shell_exec()`, `exec()`, `system()`, `passthru()`. Indicators: `cmd=`/`exec=` in queries, repeated hits on one file, double extensions (`image.jpg.php`), web server spawning shells. **Auditd** — Linux audit framework (`creat`/`execve` events). **Hafnium / ProxyLogon** and **Conti** — real actors that used Exchange web shells.

**DoS vs DDoS** — denial of service from one source vs many (a **botnet**). **Layer 7** — application-layer attacks. **Slowloris** — partial requests tie up connections. **HTTP Flood** — huge request volume. **Cache Bypass** — random query strings (`/products?a=abcd`) force the origin to respond. **Denial of Wallet** — driving up the victim's cloud bill. Signs: high request rate, odd User-Agents, global IPs, burst timestamps, 5xx spikes, expensive endpoints (`/login`, `/search`, `/checkout`).
