# TryHackMe — Humans as Attack Vectors

**Path:** SOC Level 1 — Module 1: Blue Team Introduction
**Date completed:** [11/07/2026]
**Room link:** [(https://tryhackme.com/room/humansattackvectors)]

---

## 🎯 What I Learned

- Why humans are specifically targeted by attackers
- What social engineering is and the two traits that make it effective
- Common attack methods that exploit humans: phishing, malware downloads,
  deepfakes, impersonation, and other techniques
- The two key defensive tasks: Mitigation and Detection
- Practical mitigation measures a SOC/company can put in place

## 🧠 In My Own Words

Humans are targeted by attackers because of the **access** they can
provide — to websites, mailboxes, or databases. Some attackers go after a
specific target's access; others aren't selective at all, breaching as many
accounts as possible and deciding how to use them afterward.

Attacks that target humans all share one common trait: they rely on
**manipulating the victim** into helping the attacker, whether knowingly or
not. This is known as **social engineering** — it exploits human psychology
rather than technical flaws. For social engineering to succeed, it's
typically designed to be:
- **Trustworthy** — the attacker must appear legitimate so the victim trusts
  them
- **Emotional** — the attack triggers feelings like urgency, fear, or
  curiosity, pushing the victim to act quickly without thinking it through

### Common human-targeted attack methods

**Phishing** — the most common form of social engineering, with an
estimated **3.4 billion malicious emails sent daily**. A typical example:
an email claiming "your account has been compromised, click here," leading
to a fake login page that steals real credentials when entered.

**Malware downloads** — attackers trick users into installing malware
disguised as a legitimate application, often using techniques like fake
CAPTCHAs, malicious QR codes, and SEO poisoning to increase success rates.

**Deepfakes** — AI-generated video/audio is increasingly used to
impersonate family members, colleagues, or corporate partners. In one real
case, a finance worker received a deepfake video call appearing to be their
boss and was tricked into wiring **$25 million** for a fake "urgent
business deal."

**Impersonation** — even without deepfake technology, attackers succeed
simply by pretending to be someone else. Several recent ransomware attacks
began with a phone call from someone impersonating the corporate IT
department, convincing the victim to hand over account access for a "quick
system repair."

**Other methods** — USB drop campaigns, physical attacks, insider threats,
and even fake job offers are all additional risks employees face
constantly, and a SOC analyst needs to be ready to respond to any of them.

### Defending against human-targeted threats: Mitigation vs Detection

Defence involves two key tasks:
- **Mitigation** — aims to prevent or reduce the chance/impact of attacks
  in the first place (e.g. training employees, deploying anti-phishing
  tools)
- **Detection** — no matter how good mitigation is, some attacks will
  eventually slip through — this is where SOC skills become critical, to
  catch and investigate what mitigation missed

As a SOC analyst, detecting and investigating attacks is the core skill
built throughout the SOC Level 1 path. But understanding **mitigation** is
equally valuable — if proposed mitigation ideas get approved by IT and
management, it directly eases the SOC's ongoing workload and makes the
company more secure overall.

**Example mitigation measures:**

| Mitigation | Description |
|---|---|
| **Anti-phishing solution** | Blocks phishing emails before users even see them, easing SOC routine |
| **Antivirus / EDR solution** | Prevents humans from successfully running malware on corporate hosts |
| **"Trust but verify" principle** | Teaches employees to verify suspicious requests, even ones appearing to come from the "CEO" or "IT" |
| **Security awareness training** | Teaches phishing detection, reinforced through simulated phishing exercises |

## 🛠️ Key Terms Introduced

- Social engineering
- Phishing, Malware downloads, Deepfakes, Impersonation
- USB drop campaigns, Insider threats
- Mitigation vs Detection
- Anti-phishing, EDR, "Trust but verify," Security awareness training

## ❓ Questions I Had / Things to Revisit

- Want to see a real (or simulated) phishing email up close and practice
  spotting the red flags myself
- Curious how a SOC actually detects a deepfake-based attack in progress —
  is this mostly a training/awareness problem, or are there technical
  detection methods too?
- Want to understand more about how SEO poisoning specifically works to
  push malicious downloads higher in search results

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
why humans are targeted, the core social engineering methods, and the
mitigation vs detection distinction confidently.

---

*This is a great reminder that not every SOC skill is purely technical —
understanding human psychology and pushing for good mitigation measures is
just as much a part of the job as reading logs or tuning a SIEM rule.*
