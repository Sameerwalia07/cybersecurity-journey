# TryHackMe — Phishing Analysis Tools

**Path:** SOC Level 1 — Module 5: Phishing Analysis
**Date completed:** [add date]
**Room link:** [add room url]

---

## 🎯 What I Learned

- What artifacts to collect from an email header and body during analysis
- Tools for automating header analysis, IP/URL reputation checks, and
  malware sandboxing
- What PhishTool is and how it centralises a phishing investigation
- How to approach the three practical scenarios in this room step by step

## 🧠 In My Own Words

This room builds on the manual analysis skills from the previous two rooms
by introducing tools that **automate and accelerate** the same process.

### Artifacts to Collect

**From the header:**
- Sender email address (true origin)
- Sender IP address (and what a reverse lookup reveals)
- Subject line (urgency/call to action?)
- Recipient address (To/CC/BCC)
- Reply-To address (where responses actually go)
- Date and time sent

**From the body:**
- URLs/hyperlinks (expanding any shortened links)
- Attachment name(s) — suspicious names/extensions?
- Attachment hash (for threat intel lookups)

### Tools for Header Analysis

- **Google Admin Toolbox — Messageheader** and **Message Header Analyzer**
  — paste a full raw header in, and instantly extract sender IP, routing
  path, and misconfigurations, without manual parsing

### Tools for IP/URL Reputation

- **IPinfo** — quick geographic location and organisation info for an IP,
  helping judge legitimacy
- **URLScan.io** — safely "visits" a URL in a simulated browsing session,
  capturing a screenshot and full behaviour log without the analyst ever
  loading the real page
- **Talos IP & Domain Reputation Center** (Cisco) — checks whether an IP/
  domain/network has a history of malicious activity

### Tools for Extracting/Analysing Links

- Right-click → **"Copy link address"** — the simplest manual method,
  revealing the destination without clicking
- **URL extraction tools** (e.g. convertcsv's URL extractor) or
  **CyberChef's Extract URLs** operation — paste raw email content, auto-
  parse every embedded link, catching hidden/obfuscated ones a manual scan
  might miss

### Tools for Attachment Analysis

Attachments should **only ever be opened in a controlled environment**
(lab machine/sandbox) — never directly on a real device. Once safely
obtained:
- Generate a hash (e.g. `sha256sum` on Linux) for reputation lookups
- **VirusTotal** — checks files/URLs/IPs/domains against dozens of
  security vendors at once, showing detection results clearly

**Malware sandboxes** — let analysts safely detonate a file and observe its
real behaviour without needing deep malware analysis expertise:
- **ANY.RUN** — interactive sandbox; you can actively interact with the
  environment while observing processes, network activity, and system
  changes live
- **Hybrid Analysis** — free sandbox providing detailed behaviour reports
  (system changes, network activity, IOCs)
- **JOESandbox** — performs both static and dynamic analysis, producing
  comprehensive behaviour/threat classification reports

### PhishTool — Centralising the Investigation

**PhishTool** automates much of the manual work covered above, combining
threat intel, OSINT, email metadata, and automated workflows into one
platform. Key features:
- Shows the **rendered HTML**, **raw HTML**, and **message source** side
  by side upon upload
- Tabs for authentication results, transmission path, and embedded URLs
- Built-in **attachment review**
- **VirusTotal integration** directly inside the tool — no need to
  manually cross-reference
- A formal **case resolution workflow** — marking the email malicious,
  flagging key artifacts (sender, IP, URLs), adding investigation notes,
  and clicking **Resolve** — mirroring real SOC documentation practices

---

## 🔍 How I Would Approach the Three Scenarios

### Scenario 1: "Your Account Is on Hold" (L1 Triage Role-Play)

Stepping into the L1 analyst role for a user-reported email:
1. **Collect header artifacts first** — run the raw header through
   Message Header Analyzer to get the true sender IP and routing path,
   confirming the "Netflix billing" display name doesn't match the actual
   sending domain
2. **Check IP/domain reputation** — plug the sender IP into IPinfo and
   Talos to see if it's tied to known malicious infrastructure
3. **Extract and check any embedded URL** — use CyberChef's URL
   extraction or manually copy the link address, then verify it through
   URLScan.io without visiting it directly
4. **Hash the PDF attachment** and check it against VirusTotal for known
   detections
5. **Document findings** — in a real SOC (or PhishTool), mark this as a
   **True Positive**, note the spoofed sender, malicious URL, and
   attachment hash as key artifacts, then resolve the case with notes that
   could inform a future detection rule (e.g. flagging similar spoofed
   display names)

### Scenario 2: "Update Payment Details" (ANY.RUN Sandbox Analysis)

Investigating the malicious PDF attachment from the Netflix-themed email
using the provided ANY.RUN sandbox task:
1. **Open the sandbox report** and start with the **process tree** — look
   for what process actually opens/handles the PDF, and whether it spawns
   any unexpected child processes (e.g. a PDF reader launching a script
   interpreter would be a major red flag)
2. **Check network activity** — look for any outbound connections the
   file makes once opened; note destination IPs/domains, since these are
   key IOCs
3. **Review file/registry changes** — check if the sandbox logs show any
   dropped files, registry modifications, or persistence attempts
4. **Note the verdict/score** ANY.RUN assigns, and cross-reference any
   flagged IOCs (IPs, domains, hashes) against VirusTotal for additional
   confirmation
5. **Summarise behaviour** — document what the attachment actually does
   when opened (e.g. redirects to a credential harvesting page, attempts a
   payload download) as the basis for the investigation report

### Scenario 3: "Excel Executable" (ANY.RUN Sandbox Analysis)

Investigating a different malicious attachment (Excel-based) via its own
ANY.RUN sandbox task:
1. **Review the process tree** — Excel spawning something like
   `regasms.exe`, PowerShell, or `cmd.exe` is a critical red flag, since
   Excel has no legitimate reason to launch those directly
2. **Check network connections** — identify any C2 callback attempts or
   payload download URLs triggered after the macro/link executes
3. **Look at file system/registry activity** — check for dropped
   executables, persistence mechanisms (run keys, scheduled tasks), or
   attempts to disable security tools
4. **Note any errors in execution** — as seen in the earlier walkthrough
   sample, a failed execution (e.g. a system error) still reveals clear
   malicious *intent* even if the payload didn't fully run in that
   specific environment
5. **Map findings to potential impact** — persistence, data exfiltration,
   or ransomware deployment, and document all IOCs (file hash, dropped
   filenames, network indicators) for the final report

## 🛠️ Key Terms Introduced

- Messageheader, Message Header Analyzer
- IPinfo, URLScan.io, Talos IP & Domain Reputation Center
- VirusTotal, `sha256sum`
- ANY.RUN, Hybrid Analysis, JOESandbox
- PhishTool

## ❓ Questions I Had / Things to Revisit

- Want hands-on time actually running a file through ANY.RUN or Hybrid
  Analysis myself (using a safe, known sample) to get comfortable reading
  a sandbox report
- Want to try PhishTool's free tier to see the full artifact/resolution
  workflow firsthand
- Curious how a real SOC decides which sandbox tool to standardise on —
  is it usually based on cost, integration, or reporting depth?

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can
describe the tools available at each stage of investigation and walk
through a structured approach to all three practical scenarios.

---

*This room ties the whole Phishing Analysis module together — Fundamentals
gave the theory, Emails in Action showed real patterns, and this room
gives the actual toolkit to move from "I think this is phishing" to "here
are the confirmed IOCs and here's my documented verdict," which is exactly
the L1 workflow from the SOC Team Internals module applied to a specific
alert type.*
