# TryHackMe — Phishing Emails in Action

**Path:** SOC Level 1 — Module 5: Phishing Analysis
**Date completed:** [23/07/26]
**Room link:** https://tryhackme.com/room/phishingemails2rytmuv

---

## 🎯 What I Learned

Six real-world phishing sample walkthroughs, each demonstrating different
attacker techniques: spoofing, URL shortening, tracking pixels,
multi-stage redirection chains, malicious attachments, BCC abuse, and
malicious Excel payloads.

## 🧠 In My Own Words

This room moved from theory into practice — analysing six real phishing
samples to see how the "red flags" from Phishing Analysis Fundamentals
actually show up in the wild.

### Sample 1: "Cancel Your Order" (PayPal Impersonation)

**Techniques used:** spoofed sender address, URL shortening, branded HTML

- **From address mismatch:** displayed as `service@paypal.com` but actually
  sent from `gibberish@sultanbogor.com`
- **Urgency:** fake transaction receipt designed to prompt a quick reaction
- **The "Cancel the order" button** led to a **shortened URL**, hiding the
  real destination
- **Key lesson:** never interact with a shortened link directly — tools
  like **WhereGoes** can reveal the real destination without visiting it

### Sample 2: "Track Your Package" (Shipping Notification)

**Techniques used:** spoofed sender, pixel tracking, link manipulation

- **From address mismatch:** displayed as "Distribution Center" but
  actually sent from `contact@beginpro.club`
- **Hyperlink** matched the fake tracking number theme, hiding its true
  destination
- **Tracking pixel:** a hidden image (`Tracking.png`) embedded in the raw
  source, used to notify the attacker once the email is opened — exactly
  why Yahoo automatically blocked the images and disabled hover-links in
  this sample

### Sample 3: "Download Document Here" (Multi-Stage Credential Harvesting)

**Techniques used:** artificial urgency, brand impersonation (layered),
link redirection chain, credential harvesting

- **Urgency:** the download link was set to expire the same day it was sent
- **Attack chain:** clicking "Download Document Here" → fake OneDrive
  landing page → redirected again to a fake Adobe page → finally a **fake
  login portal** asking the victim to sign in with their email provider
  (e.g. Outlook)
- **The trap:** entering credentials (real or fake) always resulted in a
  generic error, because the page was never actually authenticating
  anything — it just captured and forwarded whatever was typed to the
  attacker's server
- **Key lesson:** obvious grammar/formatting mistakes existed here, but
  with AI-generated content, these tells are becoming far less reliable

### Sample 4: "Your Account Is on Hold" (Netflix Impersonation)

**Techniques used:** spoofed sender, urgency, brand impersonation, poor
grammar/typos, malicious attachment (instead of a direct link)

- **From display name:** "Netflix billing" (note the misspelling) didn't
  match the actual sender domain
- **Attack vector shift:** this sample used a **PDF attachment** rather
  than a direct link — the PDF contained an embedded "Update Payment
  Account" link pointing to a non-Netflix domain
- Additional red flags: an atypical phone number format, and abuse of a
  *legitimate* Netflix help-center domain reference to build false trust

### Sample 5: "Your Recent Purchase" (Apple Impersonation, BCC Abuse)

**Techniques used:** spoofed sender, BCC recipient, urgency, poor
grammar/typos, malicious `.dot` attachment

- **Blank email body** — unusual on its own, relying entirely on the
  attachment to carry the attack
- **Recipient was BCCed**, not directly addressed — a technique used to
  hide the true recipient list
- **Attachment:** a `.dot` file (Microsoft Word Template) — an unusual
  format for a "receipt," which itself is a red flag
- Clicking the embedded image inside the document redirected to a phishing
  site with an unusually long, complex URL despite using familiar terms
  like "apps" and "ios" to appear legitimate

### Sample 6: "Scheduled Shipment" (DHL Impersonation, Malicious Excel)

**Techniques used:** spoofed sender, brand impersonation, malicious `.xlsx`
attachment triggering executable code

- **Geographic inconsistencies as a red flag:** sender used a German
  domain, the invoice was addressed to a city in India, but the document
  content itself was written in **Mandarin** — three mismatched signals in
  one file
- Clicking the link inside the Excel document attempted to download and
  execute a payload named `regasms.exe` (blocked by a system error in this
  sample, but showing clear malicious intent)
- **If successfully executed, potential impact:**
  - **Persistence** — backdoor or scheduled task to survive a reboot
  - **Data exfiltration** — stealing files, credentials, browser-saved
    passwords
  - **Ransomware deployment** — encrypting the system for ransom

## 🛠️ Key Terms Introduced

- URL shortening abuse, WhereGoes (link expansion tool)
- Tracking pixels
- Multi-stage redirection chains
- Credential harvesting portals
- BCC abuse in phishing
- `.dot` file abuse, malicious `.xlsx` payloads

## ❓ Questions I Had / Things to Revisit

- Want to try using WhereGoes (or a similar tool) myself on a safely
  sandboxed shortened URL
- Curious how a SOC would actually detect a tracking pixel being loaded —
  is this visible in proxy/email gateway logs?
- Want to look closer at how `.dot`/`.xlsx` macro-based payloads get
  detected by modern email security gateways before they even reach an
  inbox

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through all six samples and identify the specific technique(s) used in
each with confidence.

---

*Seeing six real variations back to back really drives home that phishing
red flags follow patterns, even as the specific delivery method changes
(links vs PDFs vs Word templates vs Excel macros). This gives me a much
better mental checklist to run through when looking at a real suspicious
email going forward.*
