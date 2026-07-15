# TryHackMe — Digital Forensics Fundamentals

**Path:** Cyber Security 101
**Date completed:** [15/06/2026]
**Room link:** https://tryhackme.com/room/digitalforensicsfundamentals

---

## 🎯 What I Learned

- What digital forensics is and how it relates to broader forensics and
  cybercrime
- The four-step forensic methodology
- What proper evidence acquisition requires (authorization, chain of
  custody, write blockers)
- The two main types of Windows forensic images
- Tools commonly used in digital forensic investigations

## 🧠 In My Own Words

**Forensics** in general is the application of methods and procedures to
investigate and solve crimes. **Digital forensics** is the specific branch
of forensics focused on investigating **cyber crimes** — any criminal
activity conducted on or using a digital device. Digital forensics uses
tools and techniques to thoroughly investigate devices after an incident, in
order to find and analyse evidence that can support necessary legal action.

**The forensic methodology** follows four key stages:
1. **Collection** — gathering the evidence/data from affected devices
2. **Examination** — processing the collected data to identify relevant
   information
3. **Analysis** — interpreting that information to understand what actually
   happened
4. **Reporting** — documenting findings clearly, since this may need to hold
   up as evidence in a legal setting

**Evidence acquisition** has to be done properly to remain valid and
trustworthy:
- **Proper authorization** — investigators must have the legal right to
  collect the evidence in the first place
- **Chain of custody** — a documented, unbroken record of who has handled
  the evidence, when, and how, ensuring it hasn't been tampered with
- **Write blockers** — hardware/software tools that prevent any
  modification to the original evidence (like a hard drive) while it's being
  examined, so the original data stays perfectly intact

**Windows forensics** typically involves creating two kinds of images from
a target system:
- **Disk image** — a full, exact copy of a system's storage drive
- **Memory image** — a snapshot of the system's RAM at a point in time,
  which can reveal running processes, open connections, and other
  volatile data that would be lost on shutdown

**Tools introduced:**
- **FTK Imager** — used for creating forensic disk images
- **Autopsy** — a forensic analysis platform for examining disk images
- **DumpIt** — used for quickly capturing a memory image
- **Volatility** — a framework for analysing memory dumps/images

## 🛠️ Key Terms Introduced

- Digital forensics
- Forensic methodology: Collection, Examination, Analysis, Reporting
- Chain of custody
- Write blocker
- Disk image vs Memory image
- FTK Imager, Autopsy, DumpIt, Volatility

## ❓ Questions I Had / Things to Revisit

- Want to actually try creating a memory image with DumpIt and analysing it
  in Volatility hands-on, since this seems like a core forensic skill
- Want to understand what specifically breaks "chain of custody" in
  practice — what mistakes actually invalidate evidence?
- Curious how disk imaging and memory imaging complement each other in a
  real investigation — do you always need both?

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
the four-stage methodology, evidence acquisition requirements, and the
purpose of each tool mentioned confidently.

---

*This connects well to Incident Response — forensics feels like the deeper,
after-the-fact investigation that often follows once an incident has been
contained, so I want to keep this room's concepts in mind as I move into
that one next.*
