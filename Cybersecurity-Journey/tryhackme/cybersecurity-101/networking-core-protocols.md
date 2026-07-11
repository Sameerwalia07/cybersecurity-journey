# TryHackMe — Networking Core Protocols

**Path:** Cyber Security 101
**Date completed:** [06/06/2026]
**Room link:** https://tryhackme.com/room/networkingcoreprotocols

---

## 🎯 What I Learned

- How DNS resolves domain names, and its associated record types and tools
- How HTTP/HTTPS methods work at the protocol level
- The core commands and port numbers behind FTP, SMTP, POP3, and IMAP
- How each protocol's commands map to its specific purpose (transferring
  files vs sending mail vs retrieving mail)

## 🧠 In My Own Words

This room went deeper into the actual protocols that make up everyday
network activity — not just what they do, but the specific commands and
ports behind each one.

**DNS (Domain Name System)** is responsible for mapping a domain name to an
IP address. It operates at the **Application layer** and uses **UDP and TCP
on port 53**. Key record types include **A** (IPv4), **AAAA** (IPv6),
**CNAME** (alias to another domain), and **MX** (mail server). Useful tools
for querying DNS include `nslookup` and `whois`.

**HTTP/HTTPS** run on **port 80 (HTTP)** and **port 443 (HTTPS)**. The core
methods are **GET** (retrieve), **POST** (submit data), **PUT** (update), and
**DELETE** (remove) — these define the type of action being requested from
a web server.

**FTP (File Transfer Protocol)** runs on **port 21** and is specifically
designed for transferring files between a client and server. Its core
commands include:
- `USER` / `PASS` — authenticate to the server
- `STOR` — upload (store) a file to the server
- `RETR` — download (retrieve) a file from the server

**SMTP (Simple Mail Transfer Protocol)** runs on **port 25** and defines how
a mail client talks to a mail server, and how mail servers talk to each
other to relay messages. Core commands:
- `HELO` — initiate the conversation with the mail server
- `MAIL FROM` — specify the sender
- `RCPT TO` — specify the recipient
- `DATA` followed by the message, ending with a single `.` on its own line

**POP3 (Post Office Protocol)** runs on **port 110** and is designed to let
a client connect to a mail server and **retrieve** email messages (typically
downloading and removing them from the server). Core commands:
- `USER` / `PASS` — authenticate
- `STAT` — check mailbox status
- `LIST` — list messages
- `RETR` — retrieve a specific message
- `DELE` — delete a message
- `QUIT` — end the session

**IMAP (Internet Message Access Protocol)** runs on **port 143** and, unlike
POP3, allows **synchronising** actions across devices — reading, deleting,
and moving messages while keeping them on the server rather than only
downloading locally. Core commands:
- `LOGIN` — authenticate
- `SELECT` — choose a mailbox/folder
- `FETCH` — retrieve a message
- `COPY` / `MOVE` — copy or move a message between folders
- `LOGOUT` — end the session

## 🛠️ Key Terms / Ports Introduced

| Protocol | Port | Purpose |
|---|---|---|
| DNS | 53 (UDP/TCP) | Domain name → IP resolution |
| HTTP | 80 | Web traffic (unencrypted) |
| HTTPS | 443 | Web traffic (encrypted) |
| FTP | 21 | File transfer |
| SMTP | 25 | Sending mail |
| POP3 | 110 | Retrieving mail (download & remove) |
| IMAP | 143 | Retrieving & syncing mail (stays on server) |

## ❓ Questions I Had / Things to Revisit

- Want to understand the practical difference in real use cases: why would
  an organisation choose POP3 vs IMAP for their mail setup?
- Curious how these protocols show up in packet captures — want to try
  spotting FTP or SMTP commands directly in a Wireshark capture once I get
  to that room
- FTP transmits credentials in plaintext by default — want to confirm this
  and understand what the secure alternative (SFTP/FTPS) looks like

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through each protocol's port, purpose, and core commands confidently.

---

*This room feels like a direct bridge into log analysis later — SOC
analysts regularly look at logs referencing these exact ports and protocols
(e.g. spotting unusual traffic on port 21 or 25), so having the command-level
detail here should make those logs much less abstract.*
