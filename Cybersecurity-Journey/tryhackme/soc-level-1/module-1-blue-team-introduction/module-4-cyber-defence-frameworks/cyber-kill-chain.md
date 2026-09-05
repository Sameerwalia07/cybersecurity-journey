# TryHackMe — Cyber Kill Chain

**Path:** SOC Level 1 — Module 4: Cyber Defence Frameworks
**Date completed:** [19/07/2026]
**Room link:** [https://tryhackme.com/room/cyberkillchain]

---

## 🎯 What I Learned

- Where the Cyber Kill Chain concept comes from and why it matters
- All 7 phases of the Kill Chain, walked through using a fictional attacker
  scenario ("Megatron")
- Real tools, techniques, and MITRE ATT&CK references at each phase
- Detection signs to watch for during exploitation and installation

## 🧠 In My Own Words

The term **"kill chain"** originates from the military — describing the
structure of an attack: identify the target, decide to attack, then
destroy it. **Lockheed Martin** adapted this into the **Cyber Kill Chain®**
in 2011, defining the steps an adversary must go through in cyberspace to
succeed. Understanding it helps defend against ransomware, breaches, and
APTs (Advanced Persistent Threats) — and helps a SOC analyst assess
security gaps and recognise intrusion attempts by understanding what an
attacker is actually trying to achieve.

To make this concrete, I'll walk through the fictional attacker
**"Megatron"** progressing through each phase.

### 1. Reconnaissance

The research/planning phase — gathering infrastructure details, employee
data, business processes, and exposed technologies. Usually **passive and
undetected**. Poor recon leads to sloppy attacks; good recon enables highly
targeted, believable payloads.

- **Passive recon** — no direct interaction (WHOIS lookups, social media
  scraping, breach data review)
- **Active recon** — direct contact (social engineering, port scanning,
  banner grabbing)

**OSINT (Open-Source Intelligence)** sources: search engines, print/online
media, social media, forums/blogs, public record databases, WHOIS data.

**Megatron's move:** conducts **email harvesting** (gathering addresses for
a future phishing attack), using tools like:
- **theHarvester** — gathers emails, names, subdomains, IPs, URLs
- **Hunter.io** — finds contact info tied to a domain
- **OSINT Framework** — categorised directory of OSINT tools

### 2. Weaponization

Turning raw recon into an actual attack tool. Key terms:
- **Malware** — software designed to damage, disrupt, or gain unauthorised
  access
- **Exploit** — code taking advantage of a specific vulnerability
- **Payload** — the malicious code the attacker actually runs

**Megatron's move:** buys a pre-built payload on the Dark Web rather than
writing custom malware, saving time for later phases.

**Common weaponization tactics:**
- Infected Office documents with malicious macros/VBA
- Malicious payloads/worms implanted on USB drives for public distribution
- Setting up **C2 infrastructure** in advance
- Backdoors to bypass security mechanisms
- Tailored phishing templates or fake OAuth-consent apps

### 3. Delivery

Choosing how to transmit the payload to the target:
- **Phishing email** — spear phishing (targeted) or broad phishing,
  containing a malicious link/attachment
- **USB drops** — physically distributed in public places; can be made
  more convincing (e.g. branded with a company logo and mailed in)
- **Watering hole attacks** — compromising a website the target group
  regularly visits, redirecting them to malware (drive-by download), e.g.
  a fake browser extension pop-up

### 4. Exploitation

The moment the attacker's code actually executes, exploiting a
vulnerability:
- **Malicious macro execution** — e.g. ransomware triggered by opening a
  phishing attachment
- **Zero-day exploits** — unknown, unpatched flaws, undetectable initially
- **Known CVEs** — exploiting unpatched public vulnerabilities

After access, the attacker may escalate privileges or move laterally.

**Signs of exploitation to watch for:**
- Unexpected process spawns
- Registry changes or new services created
- Suspicious command-line arguments in system logs

### 5. Installation

Establishing **persistence** so the attacker can regain access even if
detected or the initial foothold is patched:

- **Web shell** — a malicious script (PHP, ASP, JSP) on a web server,
  often hard to detect due to its simplicity and common file extensions
- **Backdoor** — e.g. **Meterpreter** (a Metasploit payload) giving an
  interactive remote shell
- **Malicious Windows services** (MITRE **T1543.003**) — creating/modifying
  services using tools like `sc.exe` or `Reg`, sometimes **masquerading**
  the payload under a legitimate-sounding service name
- **Run keys / Startup folder entries** — ensuring the payload executes on
  every login (both per-user and system-wide startup locations exist)
- **Timestomping** (MITRE **T1070.006**) — modifying file timestamps to
  evade forensic detection and make malware look like a legitimate,
  long-standing file

### 6. Command and Control (C2)

Megatron opens a C2 channel to remotely control the compromised machine.
The infected host **"beacons"** — repeatedly communicating with the C2
server. IRC was the traditional channel but is now easily detected.

**Common modern C2 channels:**
- **HTTP (port 80) / HTTPS (port 443)** — blends with legitimate traffic,
  helping evade firewalls
- **DNS** — constant DNS requests to an attacker-controlled server, known
  as **DNS Tunneling**

Note: the C2 infrastructure itself might belong to the adversary, or to
another already-compromised host.

### 7. Actions on Objectives (Exfiltration)

The final phase — achieving the actual goal with hands-on-keyboard access:
- Collecting user credentials
- Privilege escalation (e.g. gaining domain admin from a workstation)
- Internal reconnaissance
- Lateral movement across the environment
- Collecting and exfiltrating sensitive data
- Deleting backups/shadow copies (Microsoft's snapshot/backup technology)
- Overwriting or corrupting data

## 🛠️ Key Terms Introduced

- OSINT, Passive vs Active Recon
- Malware, Exploit, Payload
- C2 (Command and Control), Beaconing, DNS Tunneling
- Web shell, Meterpreter, Timestomping
- MITRE T1543.003, T1070.006

## ❓ Questions I Had / Things to Revisit

- Want to look at a real MITRE ATT&CK technique page (e.g. T1543.003) in
  full to see how much operational detail is documented there
- Curious how defenders specifically detect DNS tunneling in practice —
  what does anomalous DNS traffic actually look like in a SIEM?
- Want to try theHarvester or the OSINT Framework hands-on in a safe/legal
  context to see real reconnaissance output

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through all 7 phases with the Megatron scenario and give real technique
examples for each.

---

*This connects directly to the Pyramid of Pain — each Kill Chain phase
produces different types of indicators (hashes at Weaponization, C2
domains/IPs at Command and Control, TTPs across all phases), so combining
both frameworks gives a much fuller picture of where and how to detect an
attack early.*
