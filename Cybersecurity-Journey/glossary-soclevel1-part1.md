# 📖 Glossary — SOC Level 1 (Part 1: Modules 1–4)

A one-stop revision and quick-reference file for the first half of TryHackMe
SOC Level 1: **Blue Team Introduction, SOC Team Internals, Core SOC
Solutions and Cyber Defence Frameworks.** Plain-English definitions with
short scenarios where they help.

> 💡 **How to use:** skim a section before an interview or a related room.
> Terms already covered in the Cyber Security 101 glossary are kept short
> here; the focus is on how they're used in a SOC.
> **Part 2** (Modules 5–8) is in `glossary-soclevel1-part2.md`. New modules
> will be added as they are completed.

## 🔎 Quick A–Z Index

- "Trust but verify" *(Module 1)*  
- Alert Fatigue *(Module 3)*  
- Alert Prioritisation *(Module 2)*  
- Alert Properties *(Module 2)*  
- Alert Reporting — the Five Ws *(Module 2)*  
- Alerts Count (AC) *(Module 2)*  
- Attack Vector *(Module 1)*  
- Blue Team *(Module 1)*  
- C2 (Command and Control) *(Module 4)*  
- CAR (Cyber Analytics Repository) *(Module 4)*  
- CIRT / CSIRT / CERT *(Module 1)*  
- Crisis Communication *(Module 2)*  
- Cyber Kill Chain (Lockheed Martin) *(Module 4)*  
- Dashboard / Visualisation *(Module 3)*  
- Deepfake *(Module 1)*  
- Detection Rule *(Module 3)*  
- Digital Forensics Analyst *(Module 1)*  
- EDR (Endpoint Detection and Response) *(Module 3)*  
- EDR Detection Methods: *(Module 3)*  
- EDR Response Actions *(Module 3)*  
- Elastic Stack (ELK) *(Module 3)*  
- Enrichment *(Module 2)*  
- Escalation *(Module 2)*  
- Event vs Alert *(Module 2)*  
- Fast Flux *(Module 4)*  
- Impersonation *(Module 1)*  
- Incident Responder *(Module 1)*  
- Insider Threat *(Module 1)*  
- IPS (Intrusion Prevention System) *(Module 1)*  
- Junior Security Analyst / SOC Level 1 (L1) Analyst *(Module 1)*  
- L2 Analyst / Senior Analyst *(Module 1)*  
- Log Correlation *(Module 3)*  
- Malware *(Module 4)*  
- Misconfiguration *(Module 1)*  
- Mitigation vs Detection *(Module 1)*  
- MITRE ATT&CK *(Module 4)*  
- MITRE tactic IDs: *(Module 4)*  
- MSSP (Managed Security Services Provider) *(Module 1)*  
- MTTD (Mean Time To Detect) *(Module 2)*  
- OSINT *(Module 4)*  
- Patch *(Module 1)*  
- Penetration Test *(Module 1)*  
- Phishing *(Module 1)*  
- Pyramid of Pain *(Module 4)*  
- Security Awareness Training *(Module 1)*  
- SIEM *(Module 2)*  
- SIEM (Security Information and Event Management) *(Module 3)*  
- SLA (Service Level Agreement) *(Module 2)*  
- SOAR *(Module 3)*  
- SOC (Security Operations Centre) *(Module 1)*  
- SOC Team Availability *(Module 2)*  
- Social Engineering *(Module 1)*  
- Splunk *(Module 3)*  
- Supply Chain Attack *(Module 1)*  
- Threat Modelling *(Module 4)*  
- True Positive (TP) *(Module 2)*  
- Unified Kill Chain (UKC) *(Module 4)*  
- USB Drop Campaign *(Module 1)*  
- Vulnerability *(Module 1)*  
- Web Shell *(Module 4)*  
- Workbook / Playbook / Runbook *(Module 2)*  
- YARA *(Module 4)*  
- Zero-day *(Module 1)*

---

## Module 1 — Blue Team Introduction

**Blue Team** — the defenders: people who protect an organisation by monitoring, detecting and responding to threats. Contrast with **Red Team** (simulates attackers) and **GRC** (Governance, Risk and Compliance: policies, audits, regulations).

**SOC (Security Operations Centre)** — the team (and room) that monitors an organisation's systems 24/7, detects threats and starts the response.

**Junior Security Analyst / SOC Level 1 (L1) Analyst** — the first line of the SOC. Triages alerts, decides true or false positive, and escalates real threats to L2.
*Scenario: At 3 a.m. a SIEM alert fires for 40 failed logins. L1 checks the source IP and account, confirms it looks like a brute force, and escalates to L2 with notes.*

**L2 Analyst / Senior Analyst** — takes escalated incidents and investigates deeper. **SOC Engineer** builds and tunes the tools (SIEM rules, integrations). **SOC Manager** runs the team and reports to leadership.

**Incident Responder** — contains, eradicates and recovers from confirmed incidents.

**CIRT / CSIRT / CERT** — Computer (Security) Incident Response Team: a dedicated team for handling security incidents.

**MSSP (Managed Security Services Provider)** — an external company that runs security monitoring for other organisations.

**Digital Forensics Analyst** — recovers and analyses evidence (disks, memory, logs) to reconstruct what happened. **Threat Intelligence Analyst** — tracks adversaries and their TTPs. **AppSec Engineer** — secures applications during development.

**Attack Vector** — the route an attacker uses to get in. This module covers two big ones: **humans** and **systems**.

**Social Engineering** — manipulating people (not machines) into giving access or information.

**Phishing** — fraudulent messages that trick a user into clicking, opening or entering credentials.

**Deepfake** — AI-generated fake audio/video used to impersonate someone convincingly.

**Impersonation** — pretending to be a trusted person (CEO, IT support, a vendor).

**USB Drop Campaign** — leaving infected USB drives where employees will find and plug them in.

**Insider Threat** — risk from someone with legitimate access (malicious or careless).

**Mitigation vs Detection** — *mitigation* reduces the chance or impact of an attack (anti-phishing filters, patching); *detection* notices it is happening (alerts, EDR). Good defence needs both.

**"Trust but verify"** — don't assume a request is genuine because it looks internal: confirm through a second channel.

**Security Awareness Training** — teaching staff to recognise attacks; the main defence against human attack vectors.

**Vulnerability** — a weakness that can be exploited. **CVE (Common Vulnerabilities and Exposures)** — the public ID for a known vulnerability, e.g. `CVE-2017-5638` (Apache Struts).

**Zero-day** — a vulnerability with no patch available yet (and often no signature).

**Supply Chain Attack** — compromising a trusted vendor or software update to reach many customers.

**Misconfiguration** — insecure settings (default passwords, open storage, wrong permissions). Often the easiest way in.
*Scenario: A cloud storage bucket accidentally set to "public" exposes customer files without any exploit.*

**Patch** — a software update that fixes a vulnerability. **Patch management** — keeping systems updated.

**IPS (Intrusion Prevention System)** — monitors traffic and **blocks** detected threats. **WAF (Web Application Firewall)** — filters HTTP traffic to web apps.

**Penetration Test** — authorised simulated attack to find weaknesses. **Vulnerability Scan** — automated check for known weaknesses. **Configuration Audit** — checking settings against a standard such as **CIS Benchmarks** (hardening guides).

---

## Module 2 — SOC Team Internals

**Event vs Alert** — an *event* is any recorded activity (a login, a file open). An *alert* is an event (or group) a rule flagged as worth attention.

**SIEM** — collects, correlates and alerts on logs from many sources. **EDR** — monitors endpoints. **NDR (Network Detection and Response)** — monitors network traffic. **SOAR** — automates response. **ITSM (IT Service Management)** — ticketing for tracking work and incidents.

**Alert Properties** — what an alert usually shows: **Time**, **Name**, **Severity**, **Status** (new/in progress/closed), **Verdict** (true/false positive), **Assignee**, **Description**, **Fields** (IPs, users, hostnames).

**Alert Prioritisation** — deciding which alert to handle first, by severity, asset importance and context (a critical alert on a domain controller beats a low one on a test PC).

**True Positive (TP)** — the alert is real malicious activity. **False Positive (FP)** — the alert fired but the activity is benign.
*Scenario: "Port scan detected" from the IT team's own vulnerability scanner is a false positive; the same alert from an unknown external IP is a true positive.*

**Workbook / Playbook / Runbook** — documented procedures for handling alerts. *Playbook*: the overall strategy and decisions; *runbook*: the exact technical steps; *workbook* (as used here): a step-by-step checklist per alert type, typically **Enrichment → Investigation → Escalation**.

**Enrichment** — adding context to an alert (is this IP known-bad? who owns the host?). **Lookups** use these sources: **Identity inventory** (users and roles), **Asset inventory** (hosts, owners, criticality) and **Network diagram** (how systems connect).

**Escalation** — handing a confirmed threat to a higher tier with a clear report.

**Alert Reporting — the Five Ws** — **Who** (user/host), **What** (what happened), **When** (time), **Where** (system/network location), **Why** (why it is suspicious/likely intent). A good report lets L2 act without re-investigating.

**Crisis Communication** — predefined procedures for who to tell (and how) during a major incident.

**Alerts Count (AC)** — total alerts received; measures workload. **False Positive Rate (FPR)** — FPs ÷ total alerts; measures noise. **Alert Escalation Rate (AER)** — escalated ÷ total; reflects L1 experience. **Threat Detection Rate (TDR)** — detected threats ÷ total threats; reflects SOC reliability.

**SLA (Service Level Agreement)** — the agreed time limits for handling alerts by severity.

**MTTD (Mean Time To Detect)** — average time from the attack starting to detection. **MTTA (Mean Time To Acknowledge)** — average time from alert to an analyst picking it up. **MTTR (Mean Time To Respond/Resolve)** — average time to contain or close it. Lower is better for all three.
*Scenario: Malware runs at 09:00, the alert fires at 09:20 (detect: 20 min), L1 opens it at 09:25 (acknowledge: 5 min), the host is isolated at 10:00 (respond: 35 min).*

**SOC Team Availability** — whether enough trained analysts cover every shift (24/7).

---

## Module 3 — Core SOC Solutions

**EDR (Endpoint Detection and Response)** — an agent on each endpoint records activity and lets analysts detect and respond. **Agent/Sensor** — the software on the endpoint. **Telemetry** — the recorded data (processes, network connections, file and registry changes). **EDR Console** — the central dashboard.

**EDR Detection Methods:**
- **Behavioural Detection** — flags suspicious behaviour, not just known files. *Example: `winword.exe` spawning `powershell.exe`.*
- **Anomaly Detection** — flags deviation from the endpoint's baseline.
- **IOC Matching** — matches hashes, IPs and domains against threat intelligence.
- **MITRE ATT&CK Mapping** — labels the alert with a tactic and technique.
- **Machine Learning** — spots chains of actions that look malicious together.

**EDR Response Actions** — **Isolate Host** (cut it from the network; stops lateral movement), **Terminate Process**, **Quarantine** (move a malicious file where it can't run), **Remote Access** (shell onto the endpoint, e.g. CrowdStrike Falcon **RTR**, Real Time Response).

**SIEM (Security Information and Event Management)** — central log collection, normalisation, correlation, alerting and search. **Host-centric logs** — from endpoints (e.g. Windows Event 4688, process created). **Network-centric logs** — from network devices (firewall, proxy, DNS).

**Log Correlation** — linking events from different sources into one story.
*Scenario: a firewall shows an outbound connection to a rare IP, and 10 seconds earlier EDR showed `powershell.exe` launch from a Word file on the same host. Together: likely malicious macro and C2.*

**Detection Rule** — logic that raises an alert, e.g. `Log Source + EventID + field match → alert`.

**Splunk** — a SIEM with three components: **Forwarder** (collects and sends data), **Indexer** (parses and stores as searchable events), **Search Head** (where analysts search and visualise). **SPL (Search Processing Language)** — Splunk's pipe-based query language. **Field-value pairs / Events** — the structured form of indexed data.

**Elastic Stack (ELK)** — **Elasticsearch** (stores and searches), **Logstash** (processes and ships data), **Beats** (lightweight collectors, e.g. **Winlogbeat** for Windows logs, **Packetbeat** for network data), **Kibana** (UI). **Index Pattern** — tells Kibana which indices to query. **KQL (Kibana Query Language)** — query syntax supporting free text, wildcards, `AND`/`OR`/`NOT` and field-based search (`field: value`).

**Dashboard / Visualisation** — saved charts and tables for monitoring.

**SOAR** — **Security Orchestration, Automation and Response**. **Orchestration** connects tools, **Automation** runs tasks without humans, **Response** takes action. A **Playbook** in SOAR is an automated workflow.
*Scenario: a phishing alert triggers a SOAR playbook that extracts the URL, checks VirusTotal, and deletes the email from all inboxes if malicious.*

**Alert Fatigue** — analysts overwhelmed by too many (often false) alerts and start missing real ones. SOAR and tuning help.

---

## Module 4 — Cyber Defence Frameworks

**Pyramid of Pain** — ranks indicators by how much it hurts an attacker when you block them: **Hash values** (trivial) → **IP addresses** (easy) → **Domain names** (simple) → **Network/Host artifacts** (annoying) → **Tools** (challenging) → **TTPs** (tough). Detect higher up the pyramid for lasting impact.

**Fast Flux** — rapidly changing the IPs behind a domain to evade IP blocking. **Punycode** — encoding of non-ASCII domain characters, abused for lookalike (homograph) domains.

**YARA** — rules that identify malware by patterns in files. **Fuzzy Hashing (SSDeep)** — similarity hashing that matches files that are *almost* identical. **Pass-the-Hash** — using a stolen password hash to authenticate without cracking it.

**Cyber Kill Chain (Lockheed Martin)** — seven phases: **Reconnaissance → Weaponisation → Delivery → Exploitation → Installation → Command & Control → Actions on Objectives**. Break the chain at any step to stop the attack.

**OSINT** — Open-Source Intelligence from public sources. **Passive recon** — no contact with the target; **active recon** — directly probing it.

**Malware** — malicious software. **Exploit** — code that abuses a vulnerability. **Payload** — what the exploit delivers/runs.

**C2 (Command and Control)** — the channel by which the attacker controls infected hosts. **Beaconing** — regular check-in traffic to a C2 server. **DNS Tunnelling** — hiding data/C2 inside DNS queries.

**Web Shell** — a script uploaded to a web server giving remote command execution. **Meterpreter** — a Metasploit payload for remote control. **Timestomping** — altering file timestamps to hide activity (MITRE T1070.006). **T1543.003** — Create or Modify System Process: Windows Service (persistence).

**Unified Kill Chain (UKC)** — an 18-phase model combining the Kill Chain and ATT&CK, grouped into three goals: **In** (get in), **Through** (move through the network), **Out** (achieve the objective).

**Threat Modelling** — structured thinking about what can go wrong. **STRIDE** — threat categories (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege). **DREAD** — risk scoring. **CVSS** — the standard severity score (0–10) for vulnerabilities.

**MITRE ATT&CK** — a knowledge base of adversary behaviour. **Tactic** — the goal ("why"). **Technique** — the method ("how"). **Procedure** — a real-world implementation. Together, **TTPs**. **ATT&CK Matrix** — the table of tactics and techniques. **ATT&CK Navigator** — tool to annotate/visualise the matrix.

**MITRE tactic IDs:** TA0043 Reconnaissance, TA0001 Initial Access, TA0002 Execution, TA0003 Persistence, TA0004 Privilege Escalation, TA0005 Defence Evasion, TA0006 Credential Access, TA0007 Discovery, TA0008 Lateral Movement, TA0009 Collection, TA0010 Exfiltration, TA0011 Command and Control, TA0040 Impact.

**CAR (Cyber Analytics Repository)** — MITRE's library of detection analytics. **D3FEND** — MITRE's defensive countermeasure framework: **Model → Harden → Detect → Isolate → Deceive → Evict → Restore**. **MITRE Engage** — adversary engagement/deception framework.
