# 📖 Glossary — Terms I've Learned

A running list of terms, explained in my own words.

---
# 📖 Glossary — Pre Security Path

A one-stop revision and quick-reference file covering every major term from
the TryHackMe Pre Security path — both the rooms I wrote full deep-dive
writeups for, and terms from the remaining rooms I completed but didn't
document in depth. Organised by section to match the path structure, with
plain-English definitions and real-world scenario examples where useful.

---

## Section 1 — Introduction

**Offensive Security** — the practice of proactively simulating attacks
(pentesting, red teaming) to find weaknesses before real attackers do.
*Example: a pentester hired to break into a company's web app before it
launches.*

**Defensive Security** — preventing and detecting cyberattacks while
minimising their impact (see full writeup: `defensive-security-intro.md`).

**Blue Team** — the umbrella term for defensive security teams (SOC,
forensics, incident response, threat intel).

**Career paths in Cyber** — common entry points include SOC Analyst,
Penetration Tester, Digital Forensics Analyst, GRC Analyst, and Security
Engineer — each requiring different foundational skills but sharing the
same core knowledge base covered in this path.

---

## Section 2 — Network Fundamentals

**LAN (Local Area Network)** — a network confined to a small physical area
(e.g. a single office or home), where devices communicate directly without
needing to go through the internet.

**OSI Model** — the 7-layer framework for how data travels across a
network (see full writeup: `osi-model.md`). Quick recall:
`Physical -> Data Link -> Network -> Transport -> Session -> Presentation -> Application`
*Mnemonic: "Please Do Not Throw Sausage Pizza Away"*

**Packet** — a unit of data formatted for transmission across a network,
containing both the actual data (payload) and header information (source/
destination addresses, protocol info).

**Frame** — a Data Link layer (Layer 2) unit of data, which encapsulates a
packet with additional info like MAC addresses for local delivery.

**MAC Address** — a hardware-level address unique to a network interface,
used for local (Layer 2) device identification.

**Router** — a device that forwards data packets between different
networks, often connecting a LAN to the internet.

**Switch** — a device that connects devices within the same LAN, forwarding
data based on MAC addresses.

*Scenario: When your laptop sends a request to google.com, it first checks
if the destination is on the same LAN (via MAC address/ARP). If not, it
forwards the packet to the router, which routes it out to the internet
using IP addressing (Layer 3).*

---

## Section 3 — How The Web Works

**DNS (Domain Name System)** — translates domain names into IP addresses
(see full writeup: `dns-in-detail.md`). Key record types: **A** (IPv4),
**AAAA** (IPv6), **CNAME** (alias), **MX** (mail server), **TXT** (text
data).

**HTTP / HTTPS** — the protocol governing web communication; HTTPS adds
encryption (see full writeup: `http-in-detail.md`). Key methods: **GET,
POST, PUT, DELETE**. Key status codes: **200** (OK), **301/302**
(Redirect), **404** (Not Found), **401** (Unauthorized), **500** (Server
Error).

**URL Structure** — Scheme (`https://`) + Host (`example.com`) + Port +
Path (`/login`) + Query String (`?id=123`) + Fragment (`#section`).

**Cookies** — small pieces of data stored by the browser, used to
remember sessions/preferences between visits.

*Scenario: Typing `tryhackme.com` into a browser triggers a DNS lookup
(domain to IP), then an HTTP GET request to that IP's web server, which
responds with the page's HTML — this is "how websites work" end to end.*

---

## Section 4 — Computer Fundamentals

**CPU (Central Processing Unit)** — the "brain" of the computer, executing
instructions.

**RAM (Random Access Memory)** — fast, volatile memory used for actively
running programs/data; cleared on shutdown.

**HDD / SSD** — long-term storage; SSDs are faster, using flash memory
instead of spinning disks.

**Client-Server Model** — a networking model where a **client** (e.g.
browser) requests services/resources from a **server** (e.g. web server),
which responds.

**Virtualisation** — running multiple virtual machines (VMs) on a single
physical machine, each with its own OS, isolated from the others.
*Example: running a Kali Linux VM on a Windows host for safe testing.*

**Cloud Computing** — on-demand delivery of computing resources (servers,
storage, databases) over the internet, typically via providers like AWS,
Azure, or GCP, instead of owning physical infrastructure.

*Scenario: A company hosting its website "in the cloud" means it's running
on virtualised servers owned by AWS/Azure, rather than physical servers
in their own building.*

---

## Section 5 — Operating Systems Basics

**Operating System (OS)** — the layer between hardware and applications,
controlling how programs access hardware resources (see full writeup:
`operating-system-security.md`).

**Windows Basics** — the world's most widely used desktop OS in
enterprise environments; key components include the Registry, Task
Manager, and Control Panel/Settings.

**Linux CLI Basics** — see full writeup: `linux-cli-basics.md`. Key
commands: `pwd`, `ls -l`, `cd`, `cat`, `find`, `df -h`.

**Windows CLI Basics** — using **Command Prompt (cmd)** or **PowerShell**
to interact with Windows via text commands instead of the GUI. Common
commands: `dir` (list files), `cd` (change directory), `ipconfig` (view
network config), `tasklist` (view running processes).

**File Permissions** — rules controlling who can read/write/execute a
file. On Linux, shown as `rwx` triplets (owner/group/others), e.g. `755`.

*Scenario: A misconfigured Linux file with `777` permissions (read/write/
execute for everyone) is a classic vulnerability — any user on the system
could modify or execute it, even if they shouldn't have access.*

---

## Section 6 — Software Basics

**Data Representation** — how computers store data at the lowest level:
**binary** (0s and 1s), **hexadecimal** (base-16, often used to represent
binary more compactly, e.g. in memory addresses or color codes).

**Data Encoding** — converting data into a specific format for storage or
transmission — **not** for security (unlike encryption). Common encodings:
**Base64** (converts binary data to ASCII text, often seen in email
attachments or obfuscated scripts), **URL encoding** (`%20` for a space).

**Python (Simple Demo)** — a widely used, readable scripting language;
common in security for automation, quick tooling, and exploit scripting.

**JavaScript (Simple Demo)** — the scripting language that runs in web
browsers, enabling interactive web pages; also relevant to web security
since many attacks (XSS) exploit how JS executes in the browser.

**SQL (Structured Query Language) Basics** — the language used to query
and manage relational databases. Relevant to security via **SQL
Injection**, where malicious input manipulates a database query.

*Scenario: A login form vulnerable to SQL Injection might let an attacker
type `' OR '1'='1` into the username field to bypass authentication
entirely, because the malformed input tricks the underlying SQL query into
always evaluating as true.*

---

## Section 7 — Attacks and Defenses

**CIA Triad** — Confidentiality, Integrity, Availability — the three
pillars security revolves around (see full writeup: `the-cia-triad.md`).

**Cryptography Concepts** — the practice of securing data through
mathematical techniques:
- **Encryption** — converting readable data (plaintext) into unreadable
  form (ciphertext), reversible with the correct key
- **Symmetric encryption** — same key used to encrypt and decrypt (fast,
  but key distribution is a challenge)
- **Asymmetric encryption** — uses a public/private key pair; the public
  key encrypts, only the private key can decrypt
- **Hashing** — one-way transformation producing a fixed-size digest;
  used for integrity checking and password storage (not reversible, unlike
  encryption)

**"Become a Hacker" / "Become a Defender"** — introductory rooms framing
the two career tracks side by side: offensive (finding and exploiting
weaknesses) vs defensive (detecting and stopping exploitation) — both
requiring overlapping technical foundations but different day-to-day goals
and mindsets.

*Scenario: A password stored using proper hashing (e.g. bcrypt) means even
if the database is breached, attackers can't directly recover the original
password — but a password "encrypted" and stored with a recoverable key
could be decrypted if that key is also compromised. This is why hashing,
not encryption, is the correct choice for password storage.*

---

## 🧠 Quick Self-Test

Before moving on to SOC Level 1 content, you should be able to answer these
without looking:
- [ ] What are the 7 OSI layers, in order?
- [ ] What's the difference between TCP and UDP?
- [ ] What does an A record vs a CNAME record do?
- [ ] What are the 3 pillars of the CIA Triad, with one example attack per
      pillar?
- [ ] What's the difference between encryption and hashing?
- [ ] What Linux command shows file permissions in long format?
- [ ] What's the difference between symmetric and asymmetric encryption?

---






---

*Add new terms as you meet them. Alphabetizing isn't necessary — recency of
learning matters more than perfect organization at this stage.*
