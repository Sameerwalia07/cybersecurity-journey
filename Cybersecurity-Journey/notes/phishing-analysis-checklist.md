# Phishing Analysis Checklist — Step-by-Step Reference

A practical, run-through-it checklist for analysing a suspicious email,
pulled from the Phishing Analysis module rooms.

## Step 1 — Collect Header Artifacts

- [ ] Sender email address (does display name match actual address?)
- [ ] Sender IP address (reverse lookup / reputation check)
- [ ] Subject line (urgency or call to action?)
- [ ] Recipient address (To/CC/BCC — was it BCCed, hiding true recipients?)
- [ ] Reply-To address (does it differ from From?)
- [ ] Date and time sent

**Tools:** Google Admin Toolbox Messageheader, Message Header Analyzer

## Step 2 — Collect Body Artifacts

- [ ] All URLs/hyperlinks (expand any shortened links before trusting them)
- [ ] Attachment name(s) and extensions (anything unusual, e.g.
      `invoice.pdf.exe`, `.dot` files for a "receipt")
- [ ] Generate attachment hash (`sha256sum`) for reputation lookups

**Tools:** CyberChef (Extract URLs), WhereGoes (link expansion), URL
extraction tools

## Step 3 — Check Reputation

- [ ] IP reputation → **IPinfo**, **Talos IP & Domain Reputation Center**
- [ ] URL safety (without visiting it) → **URLScan.io**
- [ ] File/hash reputation → **VirusTotal**

## Step 4 — Sandbox Analysis (if attachment present)

- [ ] Never open attachments on a real device — use a sandbox only
- [ ] Check the **process tree** for unusual parent-child relationships
      (e.g. Word/Excel spawning PowerShell or cmd)
- [ ] Check **network activity** for outbound connections / C2 callbacks
- [ ] Check for **dropped files / registry changes / persistence**
      attempts
- [ ] Note any errors — a failed execution can still reveal malicious
      intent

**Tools:** ANY.RUN, Hybrid Analysis, JOESandbox

## Step 5 — Red Flags Checklist

- [ ] Spoofed/mismatched sender address
- [ ] Urgency or pressure language
- [ ] Brand impersonation (logos/colors mimicking a real company)
- [ ] Grammar/spelling issues (less reliable now with AI-generated content)
- [ ] Generic greeting ("Dear Customer")
- [ ] Hidden/shortened links
- [ ] Unusual attachment format for the claimed purpose
- [ ] Geographic inconsistencies (sender domain vs invoice address vs
      document language)
- [ ] Tracking pixels (check raw source for tiny embedded images)

## Step 6 — Defang Before Documenting

Always defang IOCs before writing them in a report/ticket:

```
Original:  http://www.suspiciousdomain.com
Defanged:  hxxp[://]www[.]suspiciousdomain[.]com
```

## Step 7 — Document and Resolve

- [ ] Mark verdict: True Positive / False Positive
- [ ] List all IOCs found (defanged)
- [ ] Note investigation steps taken
- [ ] Escalate if needed (see `incident-response-cheatsheet.md` escalation
      checklist)

**Tool:** PhishTool (centralises all of the above in one workflow)

---
*Run through this checklist top to bottom on any real or practice
phishing email — it's designed to match the actual L1 triage workflow
from SOC L1 Alert Triage.*
