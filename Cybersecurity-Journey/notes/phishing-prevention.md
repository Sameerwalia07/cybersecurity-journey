# TryHackMe — Phishing Prevention

**Path:** SOC Level 1 — Module 5: Phishing Analysis
**Date completed:** [add date]
**Room link:** [add room url]

---

## 🎯 What I Learned

- How SPF, DKIM, and DMARC work together to authenticate email senders
- How to read and build each type of DNS record
- What S/MIME is and how it secures individual messages
- The technical defenses organisations deploy against phishing
- The user-facing tools and training that complement technical controls

## 🧠 In My Own Words

Phishing remains one of the most common and effective ways attackers gain
initial access. Defenders counter this with a layered mix of **email
authentication standards**, **technical filtering tools**, and **user-facing
training**.

### SPF (Sender Policy Framework)

SPF authenticates the **sender** of an email — it lets receiving mail
servers verify whether the sending server is actually authorised to send on
behalf of a domain. An SPF record is a **DNS TXT record** listing
authorised sending IPs/domains.

**Verification outcomes:**

| Result | Action |
|---|---|
| Pass, Neutral, None | Accept |
| SoftFail, PermError | Flag as suspicious, but still allow |
| Fail, TempError | Reject immediately |

**Sample SPF record:**
```
v=spf1 ip4:127.0.0.1 include:_spf.google.com -all
```
- `v=spf1` — marks the start of the record
- `ip4:127.0.0.1` — an authorised sending IPv4 address
- `include:_spf.google.com` — an authorised sending domain
- `-all` — reject anything not explicitly authorised

**Tools:** SPF Surveyor (visualises DNS records), Google Admin Toolbox
Messageheader (shows SPF result directly from a header, e.g. `softfail
with IP Unknown!` — meaning the sender wasn't verified but was still
delivered, flagged as suspicious).

### DKIM (DomainKeys Identified Mail)

DKIM authenticates that a message truly came from the claimed domain, using
**digital signatures** rather than IP lists. The sending server signs the
email with a **private key**; the receiving server checks a **public key**
published in DNS to verify the signature. DKIM's key advantage over SPF:
**it survives forwarding.**

**Sample DKIM record:**
```
v=DKIM1; k=rsa; p=<public_key>
```
- `v=DKIM1` — DKIM version (optional)
- `k=rsa` — key type (RSA is standard)
- `p=` — the public key used to verify the signature

**Result example:** a spam email showing `permerror` for DKIM indicates a
permanent verification failure — could mean an invalid signature, missing/
incorrect DNS record, a modifying forwarding server, or misconfiguration.

**Tools:** dmarcian's DKIM Record Checker and Validator.

### DMARC (Domain-Based Message Authentication, Reporting, and Conformance)

DMARC ties SPF and DKIM together through **alignment** — confirming the
sender's domain actually matches what SPF and DKIM verified. If alignment
fails, DMARC tells the receiving server exactly how to handle the message
based on a defined policy.

**Sample DMARC record:**
```
v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com
```
- `v=DMARC1` — DMARC version (required)
- `p=quarantine` — policy: move failing mail to spam (other options
  include `p=reject` or `p=none`)
- `rua=` — optional: where aggregate reports get sent

**Tool:** dmarcian's Domain Checker inspects SPF, DKIM, and DMARC together
— e.g. checking `microsoft.com` shows all three passing, with a
`p=reject` policy meaning any mail failing DMARC alignment gets rejected
outright.

### S/MIME (Secure/Multipurpose Internet Mail Extensions)

S/MIME secures **individual messages** via public key cryptography,
providing two features:

**Digital Signature** (using the sender's private/public key pair):
- **Authentication** — confirms sender identity via their certificate
- **Non-repudiation** — sender can't deny sending it
- **Data Integrity** — detects any post-signing tampering

**Encryption** (using the recipient's public/private key pair):
- **Confidentiality** — only the intended recipient can decrypt it

**Worked example — Bob sending Mary a secure email:**
1. Bob creates a digital certificate to generate his Digital Signature
2. Bob signs the email with his **private key**
3. Bob shares his **public key** openly with Mary
4. Bob also requests Mary's **public key**, to encrypt the message for her
5. Mary verifies Bob's signature using Bob's **public key**
6. Mary decrypts the message using her own **private key**
7. For Mary's reply, the same process runs in reverse
8. Both now hold each other's certificates for future secure exchanges

### Reading Real SMTP/Header Authentication Results

A real email header will typically show all three results together, e.g.:
```
Authentication-Results: mx.google.com;
  spf=pass (google.com: domain designates 1.2.3.4 as permitted sender)
  dkim=pass header.i=@example.com;
  dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=example.com
```
An analyst scanning this line can immediately see all three checks passed
— versus a phishing email where one or more of these would show `fail`,
`softfail`, or `permerror`, which is often the fastest first signal that a
message deserves closer investigation.

### Technical Defenses Organisations Deploy

- **Email Filtering** — blocks/quarantines based on IP and domain
  reputation
- **Secure Email Gateways (SEGs)** — scan for impersonation, spoofing, and
  phishing techniques that basic filters might miss
- **Link Rewriting** — replaces suspicious/unknown URLs with safe,
  redirected ones, buying time to scan and verify
- **Sandboxing** — isolates and tests suspicious links/attachments in a
  secure virtual environment before they reach the user

### User-Facing Tools & Training

Since some phishing will always get through technical defenses:
- **Trust & Warning Indicators** — banners like "External Sender" or
  "Suspicious Link" to give users visual context
- **Phishing Reporting** — easy in-email reporting buttons for users to
  flag suspicious messages
- **User Awareness Training** — teaching employees to recognise phishing
  and social engineering tactics
- **Phishing Simulation Exercises** — controlled internal phishing
  campaigns to test and reinforce training

## 🛠️ Key Terms Introduced

- SPF, DKIM, DMARC (records, verification outcomes, alignment)
- S/MIME (digital signature vs encryption)
- SEG (Secure Email Gateway), Link Rewriting, Sandboxing

## ❓ Questions I Had / Things to Revisit

- Want to check a few more real domains through dmarcian's Domain Checker
  to compare policies (`p=none` vs `p=quarantine` vs `p=reject`)
- Want to look at a real phishing sample's header (from the earlier
  "Phishing Emails in Action" room) and check what its SPF/DKIM/DMARC
  results actually were
- Curious how link rewriting/sandboxing specifically integrate with
  something like Microsoft Defender for Office 365 in practice

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can
explain how SPF, DKIM, and DMARC work individually and together, walk
through the Bob/Mary S/MIME example, and list the technical and
user-facing defenses organisations use.

---

*This wraps up Module 5 nicely — Fundamentals taught email structure,
Emails in Action showed real attacker patterns, Tools gave the
investigation toolkit, and this room shows the authentication layer that
should ideally catch a lot of these spoofed senders before they even reach
an inbox. Genuinely useful to now be able to read SPF/DKIM/DMARC results
directly from a header during future investigations.*
