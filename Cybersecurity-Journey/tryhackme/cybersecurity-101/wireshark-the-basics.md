# TryHackMe — Wireshark: The Basics

**Path:** Cyber Security 101
**Date completed:** [07/06/2026]
**Room link:** https://tryhackme.com/room/wiresharkthebasics

---

## 🎯 What I Learned

- What Wireshark is and what it's used for
- The layout of the Wireshark interface and its main panes
- What packet dissection means and what information it reveals
- How to navigate, filter, and investigate captured traffic

## 🧠 In My Own Words

**Wireshark** is an open-source platform used for **packet analysis and
sniffing** — it lets you investigate live network traffic in real time, or
capture it into a file (**.pcap**) to analyse later.

**Interface layout:**
- **Toolbar** — quick access to core actions (start/stop capture, save, etc.)
- **Display filter bar** — where you type filters to narrow down which
  packets are shown, without discarding the rest of the capture
- **Capture filter** — unlike a display filter, this decides what gets
  captured *in the first place*, before the packets are even shown
- **Interface list** — lets you choose which network interface to capture
  traffic from
- **Recent files / Status bar** — quick access to previous captures and
  general capture status info

The capture itself is broken into three main panes:
- **Packet List** — the full list of captured packets, one row per packet
- **Packet Details** — a breakdown of the selected packet's fields
- **Packet Bytes** — the raw hex/byte-level view of the selected packet

**Colouring rules** automatically colour-code packets based on protocol or
condition (e.g. DNS traffic in one colour, TCP errors in another), making it
much faster to visually scan a large capture.

**Packet dissection** (also called protocol dissection) is the process
Wireshark uses to investigate a packet's details by decoding the protocols
and fields present in it. This is what lets Wireshark break a raw packet
down into readable details like:
- Frame number
- Source MAC address
- Source IP address
- Protocol
- Any protocol errors
- Application-layer protocol and application data

**Packet navigation features:**
- Packet numbers — used to reference specific packets
- **Find** — search within the capture
- **Mark** — flag specific packets of interest for quick reference
- **Comments** — attach notes to specific packets
- **Export packets/files** — save specific packets or the whole capture out
- **Time display** — control how timestamps are shown (relative, absolute, etc.)
- **Expert Info** — a summary of warnings/errors/notable events Wireshark
  flags automatically within the capture

**Packet filtering features:**
- **Apply as filter** — right-click a field/packet to instantly build a
  display filter from it
- **Conversation filter** — filter to show only packets belonging to a
  specific conversation (e.g. between two specific IPs)
- **Colorize conversation** — highlight all packets in a conversation with a
  distinct colour
- **Follow stream** — reconstructs and displays the full data exchanged in a
  TCP/UDP/HTTP conversation, in order, which is extremely useful for reading
  what was actually said/sent between two hosts
- **Filter by column** — quickly filter based on a specific column's value

## 🛠️ Key Terms Introduced

- pcap (packet capture file)
- Packet List / Packet Details / Packet Bytes panes
- Packet dissection / protocol dissection
- Display filter vs Capture filter
- Follow stream
- Expert Info

## ❓ Questions I Had / Things to Revisit

- Want to practice actual filter syntax (e.g. `ip.addr ==`, `tcp.port ==`,
  `http.request`) hands-on rather than just knowing the features exist
- Want to try "Follow TCP Stream" on a real capture to see what a
  reconstructed conversation actually looks like
- Curious how Expert Info flags things — what counts as a "warning" vs an
  "error" in Wireshark's eyes?

## ✅ Self-Check

Could I explain this to someone else without notes? **Mostly yes** — I
understand the interface and features well; actual filter syntax is what
I'd want more hands-on reps with before teaching it confidently.

---

*Wireshark feels like one of the most directly useful tools for SOC/blue
team work covered so far — packet-level investigation is a core skill for
identifying malicious traffic, and I want to build real practice time with
this tool as I go, not just know the theory.*
