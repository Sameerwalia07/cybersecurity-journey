# TryHackMe — The CIA Triad

**Path:** Pre Security
**Date completed:** [21/05/2026]
**Room link:** [https://tryhackme.com/room/theciatriad]

---

## 🎯 What I Learned

- Why protecting data has become critical in a digitalised world
- The three pillars security revolves around: **Confidentiality, Integrity,
  Availability**
- What happens when each pillar fails, and real examples tied to each

## 🧠 In My Own Words

Because of how digitalised everything has become, protecting data isn't
optional anymore — failing to do so can lead to serious consequences,
whether financial, legal, or reputational. Security as a whole revolves
around three core conditions, known as the **CIA Triad**:

**Confidentiality** ensures that sensitive data can only be accessed by
people who are actually authorized to see it. If confidentiality fails,
unauthorized individuals gain access to data they shouldn't have, which can
lead to financial loss, privacy violations, or legal consequences.
*Example: an attacker breaching a database and stealing customer personal
information.*

**Integrity** ensures that data isn't modified by unauthorized individuals.
Without integrity, data can be altered and can no longer be trusted —
sometimes with dangerous consequences depending on what the data controls or
represents.
*Example: an attacker tampering with financial records or altering medical
data, leading to serious real-world harm even if the data was never
"stolen."*

**Availability** ensures that data and services remain accessible to
authorized users whenever they need them. It's the third pillar, but it's no
less important than the other two — most businesses depend heavily on their
digital services being up and running. If those services go down, even for
a short period, it can cause serious loss for both the business and its
users.
*Example: a Denial-of-Service (DoS) attack that takes a website or service
offline, directly costing the business revenue and trust.*

What stood out to me is that these three pillars don't operate in isolation
— a single attack can often hit more than one at once (e.g. ransomware can
threaten both availability *and* confidentiality if data is also exfiltrated
before encryption).

## 🛠️ Key Terms Introduced

- Confidentiality
- Integrity
- Availability
- CIA Triad (as the foundational security framework)

## ❓ Questions I Had / Things to Revisit

- Want to map specific security controls to each pillar more precisely (e.g.
  encryption → confidentiality, hashing/checksums → integrity, redundancy/
  backups → availability) to build a clearer mental map
- Curious how real-world incidents get categorised — does an incident report
  usually name which pillar(s) were violated?

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can define
all three pillars clearly and give a real example of an attack tied to each.

---

*This feels like the most foundational concept in the whole Pre Security
path — nearly everything else (passwords, permissions, encryption, incident
response) ultimately traces back to protecting one or more of these three
pillars. Good note to keep coming back to.*
