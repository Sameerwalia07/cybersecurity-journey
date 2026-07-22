# TryHackMe — Systems as Attack Vectors

**Path:** SOC Level 1 — Module 1: Blue Team Introduction
**Date completed:** [12/07/2026]
**Room link:** [https://tryhackme.com/room/systemsattackvectors]

---

## 🎯 What I Learned

- What counts as a "system" and why protecting it matters more than
  protecting a single user
- How systems get initially compromised, and the role users play in that
- Vulnerabilities, supply chain attacks, and zero-days
- The difference between vulnerabilities and misconfigurations
- How to respond to each, and key mitigation measures for systems

## 🧠 In My Own Words

A **system** is where data actually lives — a physical server, a lab
machine, or a cloud platform like Microsoft 365 (e.g. where banks store
card data or where emails are stored). Protecting systems matters more than
protecting individual accounts because of scale: if an attacker breaches
one user's mailbox via phishing, they get **one mailbox**. If they breach
the **mail server** itself, they get **control of thousands of mailboxes**
at once.

In most serious attacks, the attacker's first goal is simply gaining access
to the target system — what happens after depends on their motivation
(stealing data, deploying ransomware, or even destructively wiping
information with no recovery path). Interestingly, nearly all attacks start
the same way, and it's often the **system's users** who unintentionally
kick things off — inserting a malicious USB found on the street,
downloading malware from pirated software, or reusing a weak password
everywhere. In fact, **81% of breaches involve stolen or breached
passwords.**

### Vulnerabilities

Every piece of software can contain security flaws. In 2024 alone, **over
40,000 vulnerabilities** were published, with **more than 300 actively
exploited** in major attacks. IT administrators can also unintentionally
increase risk through weak passwords or overly permissive access.

**Supply chain attacks** — nearly every app depends on numerous libraries;
if attackers compromise one library or app and push a malicious update, all
downstream users get compromised too. Famous real examples: **SolarWinds**
and **3CX**, which affected thousands of companies. These are especially
hard to defend against because you can't fully control every piece of
software running across your systems — even TryHackMe itself was once
affected via a supply-chain issue in a library called Lottie Player.

**Zero-days** — some vulnerabilities take years to be discovered (e.g.
**Shellshock**, a major Linux flaw that existed since 1992 but wasn't found
until 2014). In the worst case, attackers find a vulnerability *before*
defenders do — this is a **zero-day**, and detecting exploitation of one in
time relies entirely on SOC skills, since no patch exists yet. Once a
vulnerability becomes public, it's assigned a **CVE** number, starting a
race between attackers building exploits and defenders rushing to patch.

**Responding to vulnerabilities:** the real fix is always a **patch** from
the vendor. While waiting on a patch (especially for a zero-day), temporary
measures include:
- Restricting system access to only trusted IPs
- Applying any temporary mitigations the vendor provides
- Blocking known attack patterns via IPS or WAF

### Misconfigurations

Unlike a vulnerability, a **misconfiguration** isn't a flaw in the software
itself — it's a mistake in how a system was set up, often by IT, usually to
make things simpler (e.g. using "1111" instead of a proper password).

**Real-world examples:**
- A weak "123456" password exposed chat data for **64 million** McDonald's
  job applicants
- A **misconfigured AWS web application firewall** led to a breach
  affecting **106 million** bank customers (Capital One)
- Improperly configured **smart fridges** have been silently recruited into
  full-scale botnet attacks

**Responding to misconfigurations:** these don't need a software update,
just a better setup. A SOC analyst often only discovers them *after* they've
already been exploited, but in smaller companies may also take a more
proactive role, such as:
- **Penetration Testing** — hiring ethical hackers to simulate attacks and
  report findings
- **Vulnerability Scans** — periodically scanning for default passwords or
  outdated software
- **Configuration Audits** — manually reviewing systems against best
  practices like **CIS benchmarks**

Unlike humans, systems can't be "trained" to spot an attack — but IT teams
*can* be trained to configure systems correctly and avoid simple mistakes.

**Common mitigation measures for systems:**

| Mitigation | Description |
|---|---|
| **Patch Management** | Tracking and patching vulnerable systems significantly reduces successful attack chances |
| **Training for IT** | IT staff aware of misconfiguration risks are less likely to leave systems exposed |
| **Network Protection** | Restricting system access to trusted people/IPs makes breaching it much harder |
| **Antivirus Protection** | Can stop or detect many attacks, same as with human-targeted threats |

## 🛠️ Key Terms Introduced

- Vulnerability, CVE, Zero-day
- Supply chain attack
- Misconfiguration
- Patch, IPS, WAF
- Penetration testing, Vulnerability scans, Configuration audits, CIS benchmarks

## ❓ Questions I Had / Things to Revisit

- Want to look deeper into how a zero-day actually gets detected without a
  known signature — what behavioural clues would a SOC analyst rely on?
- Curious what a CIS benchmark audit actually looks like in practice — want
  to find and skim a real one for a common system (e.g. Linux server)
- Want to connect this back to Vulnerability Scanner Overview from Cyber
  Security 101 — this room gives the "why it matters" context that makes
  that tool's purpose much clearer

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
the difference between vulnerabilities and misconfigurations, real-world
examples of each, and the mitigation measures for systems confidently.

---

*This wraps up Module 1 nicely — Humans and Systems are the two core attack
surfaces, and between mitigation and detection, I can already see how my
target SOC L1 role sits right at the detection layer, catching what gets
past all these mitigation efforts.*
