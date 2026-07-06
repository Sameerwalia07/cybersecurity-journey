# TryHackMe — OSI Model

**Path:** Pre Security
**Date completed:** [10/05/2026]
**Room link:** [https://tryhackme.com/room/osimodelzi]

---

## 🎯 What I Learned

- The OSI (Open Systems Interconnection) model is a framework that standardises
  how data travels across a network
- It breaks network communication into **7 distinct layers**, each with a
  specific job
- Understanding these layers helps in troubleshooting, and later, in
  understanding where different attacks and defenses operate

## 🧠 In My Own Words

The OSI model is essentially a blueprint for how data gets from one device to
another across a network, broken into 7 layers so each part of the process
has a clear, separate responsibility:

- **Layer 1 — Physical:** the actual physical/hardware components of the
  network — cables, network cards, radio signals — anything that physically
  carries the raw bits
- **Layer 2 — Data Link:** handles physical addressing, using **MAC
  addresses** to identify devices on the same local network
- **Layer 3 — Network:** handles **routing** — getting data across different
  networks using **IP addresses** and routing algorithms like **OSPF**
- **Layer 4 — Transport:** manages how data is actually transmitted, using
  protocols like **TCP** (reliable, connection-based) or **UDP**
  (connectionless, faster but no delivery guarantee)
- **Layer 5 — Session:** once data is ready to be sent, this layer
  establishes and manages the actual **session** (connection) between the
  sending device and the destination device
- **Layer 6 — Presentation:** acts as a **translator**, converting data into
  a format the Application layer can understand (and vice versa) — e.g.
  encryption/decryption or formatting
- **Layer 7 — Application:** the layer closest to the user — this is where
  protocols are in place in the form the user actually interacts with (e.g.
  HTTP for browsing, SMTP for email)

What helped this click for me is thinking of it as a flow: physical wires and
signals (L1) → local addressing (L2) → cross-network addressing/routing (L3)
→ actual transport method (L4) → the connection itself (L5) → translating the
data (L6) → what the user actually sees/uses (L7).

## 🛠️ Key Terms Introduced

- MAC address (Layer 2)
- IP address, OSPF, routing (Layer 3)
- TCP / UDP (Layer 4)
- Session establishment (Layer 5)
- Data translation/encryption (Layer 6)

## ❓ Questions I Had / Things to Revisit

- Want to get clearer on how encapsulation/decapsulation actually works as
  data moves down through the layers on the sending side and back up on the
  receiving side
- Need to practice mapping real tools (Wireshark, ping, traceroute) to the
  specific OSI layer they operate at — this will help when I start log/packet
  analysis later

## ✅ Self-Check

Could I explain this to someone else without notes? **Mostly yes** — I can
walk through all 7 layers and what happens at each, though encapsulation is
the part I'd want to double check before teaching it confidently.

---

*This is a model I expect to come back to constantly — a lot of later
security concepts (firewalls, IDS/IPS, packet analysis) get described in
terms of "what layer they operate at," so having this solid now should pay
off later.*
