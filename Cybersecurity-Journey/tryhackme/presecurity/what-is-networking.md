# TryHackMe — What is Networking?

**Path:** Pre Security
**Date completed:** [add date]
**Room link:** https://tryhackme.com/room/whatisnetworking

---

## 🎯 What I Learned

- The OSI model and what happens at each of the 7 layers
- The difference between TCP and UDP, and when each is used
- How DNS resolution works, step by step
- What an IP address and MAC address are used for, and how they differ

## 🧠 In My Own Words

TCP is connection-oriented — before any real data is sent, the two devices do a
"three-way handshake" (SYN, SYN-ACK, ACK) to agree the connection is ready. This
guarantees data arrives and arrives in order, which is why it's used for things
like web browsing and file transfers.

UDP skips all of that — it just fires packets without checking if they arrived.
That makes it faster but less reliable, which is why it's used for things like
video calls or live streaming, where speed matters more than perfect delivery.

DNS resolution works like a phone book lookup: when I type a domain name, my
computer asks a DNS resolver, which checks (in order) root servers, then TLD
servers, then the authoritative server for that domain, until it finds the IP
address to connect to.

## 🛠️ Commands / Tools Used

```bash
ping google.com          # tests reachability and round-trip time
traceroute google.com    # shows the path packets take, hop by hop
nslookup google.com      # queries DNS to get the IP behind a domain
```

## ❓ Questions I Had / Things to Revisit

- Still fuzzy on subnetting math (CIDR notation) — need to practice this separately
- Want to understand ARP in more depth — how does a device find a MAC address
  on the local network before it can even use IP?

## ✅ Self-Check

Could I explain this to someone else without notes? **Mostly yes** — subnetting
is the one gap I'd need to fill in first.

---

### Template notes (delete this section when reusing)
Copy this file for every new room. Keep the section headers the same so your
writeups stay consistent and easy to scan later. The "In My Own Words" and
"Questions I Had" sections are the most important — they're what actually
prove understanding rather than just completion.
