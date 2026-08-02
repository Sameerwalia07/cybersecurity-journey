# TryHackMe — Introduction to EDR

**Path:** SOC Level 1 — Module 3: Core SOC Solutions
**Date completed:** [15/07/2026]
**Room link:** [https://tryhackme.com/room/introductiontoedrs]

---

## 🎯 What I Learned

- What EDR is and why it's needed beyond traditional antivirus.
- The three pillars of EDR: Visibility, Detection, Response.
- How EDR compares to AV using a real multi-stage attack scenario.
- How EDR actually works technically (agents, telemetry, console).
- The specific detection techniques EDR uses.
- Response actions available to analysts.
- What telemetry is and what gets collected.
- How EDR fits alongside other tools in the broader security ecosystem.

## 🧠 In My Own Words

**EDR (Endpoint Detection and Response)** is a security tool designed to
monitor, detect, and respond to advanced threats at the endpoint level. As
businesses rely more on digital devices, and remote work pushes many of
those devices **outside the traditional network perimeter**, a solution is
needed that protects endpoints regardless of location — that's exactly
what EDR provides.

**Common EDR solutions:** CrowdStrike Falcon, SentinelOne ActiveEDR,
Microsoft Defender for Endpoint, OpenEDR, Symantec EDR

### The Three Pillars of EDR

1. **Visibility** — EDR collects extremely detailed data from endpoints:
   process modifications, registry changes, file/folder modifications, user
   actions, and more — presented as a structured process tree with a full
   activity timeline, including historical data for threat hunting
2. **Detection** — combines signature-based detection with
   **behavior-based** detection (catching unexpected activity), machine
   learning (catching baseline deviations), and even fileless malware
   living only in memory; also supports custom IOC feeds
3. **Response** — lets analysts act directly from the EDR console: isolate
   an endpoint, terminate a process, quarantine files, or connect remotely
   to run commands independently

### Why EDR, When We Already Have Antivirus?

Both protect endpoints, but at very different depths. AV mostly relies on
**signature-based** detection, while EDR **monitors and records behavior**,
and provides **organisation-wide visibility** — if a suspicious file
appears on one endpoint, EDR checks for it across all others too.

**Scenario comparing AV vs EDR response**, across a real multi-stage
attack:

| Attack Step | AV's Response | EDR's Response |
|---|---|---|
| 1. Phishing email with malicious macro downloaded | Does nothing (no known signature) | Logs and monitors the download |
| 2. User opens the document | Does nothing (winword.exe is legitimate) | Records execution, keeps monitoring |
| 3. Macro silently spawns PowerShell | Does nothing (no known signature) | **Flags** the unusual winword.exe → PowerShell.exe parent-child relationship |
| 4. Obfuscated PowerShell downloads second-stage payload | Typically undetected | Flags the obfuscated script execution |
| 5. Payload injected into legitimate svchost.exe | Doesn't monitor memory injection | Detects the process injection |
| 6. Attacker gains remote access via outbound connection | Lacks network-level visibility | Flags svchost.exe's unexpected outbound connection |
| **Final Result** | **May be marked clean** | **Generates a full attack-chain alert, actionable from the console** |

This scenario makes the difference concrete — AV misses every single step
of a realistic attack chain because none of the individual actions match a
known signature, while EDR catches it through behavior and context at
nearly every stage.

### How EDR Actually Works

- **Agents (Sensors)** — deployed on each endpoint, acting as the "eyes and
  ears" of the EDR. They monitor activity, perform some basic
  signature/behavior detection locally, and send detailed telemetry back to
  the central console in real time
- **EDR Console** — correlates and analyses all incoming telemetry using
  complex logic and ML, matching it against threat intelligence — acting
  as the "brain" connecting individual data points into a coherent
  **detection (alert)**

### What Happens After Detection

An analyst acknowledges and prioritises the alert (EDR assigns severities:
Critical, High, Medium, Low, Informational). Investigating the highest
severity first, the analyst reviews all detail (files, processes, network
connections, registry changes) to judge **False Positive vs True
Positive**, then takes action directly within the console if needed.

### EDR Detection Techniques

- **Behavioral Detection** — observes full file behaviour rather than just
  matching signatures (e.g. flagging `winword.exe` spawning
  `PowerShell.exe` as an unusual relationship)
- **Anomaly Detection** — learns an endpoint's baseline over time and flags
  deviations (e.g. an unusual auto-start registry modification); can
  produce false positives, but gives enough context to judge legitimacy
- **IOC Matching** — matches activity against known threat intelligence
  indicators (e.g. a downloaded file's hash matching a known malicious
  executable)
- **MITRE ATT&CK Mapping** — flagged activity gets mapped to the specific
  MITRE Tactic/Technique involved (e.g. a scheduled task creation mapping
  to *Persistence → Scheduled Task/Job*), giving analysts immediate context
- **Machine Learning Algorithms** — trained on large datasets of normal vs
  malicious behaviour, catching complex, multi-step patterns (like fileless
  or multi-staged attacks) where no single action looks malicious alone

### EDR Response Actions

- **Isolate Host** — disconnects an infected endpoint from the network,
  critical for stopping lateral movement early
- **Terminate Process** — a lighter-touch option for critical hosts where
  full isolation would cause more harm than the threat itself
- **Quarantine** — moves a malicious file to an isolated location where it
  can't execute, pending review
- **Remote Access** — lets analysts remotely access an endpoint's shell for
  deeper investigation, custom actions, or running scripts (e.g.
  CrowdStrike Falcon's RTR — Real Time Response — console)

### Telemetry — the "Black Box" of an Endpoint

**Telemetry** is the detailed data EDR agents collect and send to the
console — everything needed for detection and investigation:
- **Process executions/terminations** — reveals suspicious parent-child
  relationships or unusual executables
- **Network connections** — reveals C2 communication, unusual ports, data
  exfiltration, lateral movement
- **Command line activity** — captures CMD/PowerShell commands, catching
  obfuscated scripts AV typically misses
- **File/folder modifications** — reveals data staging, ransomware
  activity, malicious file drops
- **Registry modifications** — a goldmine for spotting persistence and
  configuration tampering

Individually, these actions can look harmless — but viewed together through
detailed telemetry, they reveal the full story of an attack.

### Artefact Collection

For deeper forensic investigation or legal reporting, analysts can extract
key artefacts remotely without physically accessing the device:
- Memory Dump
- Event Logs
- Specific Folder Contents
- Registry Hives

### EDR Within the Bigger Ecosystem

A standalone EDR is powerful, but it works alongside Firewalls, DLPs, Email
Security Gateways, IAMs, and other solutions — all typically integrated
into a **SIEM**, which becomes the central point of investigation for
analysts.

## 🛠️ Key Terms Introduced

- EDR, Agent/Sensor, Telemetry, EDR Console
- Behavioral Detection, Anomaly Detection, IOC Matching, MITRE ATT&CK Mapping
- Isolate Host, Terminate Process, Quarantine, Remote Access
- CrowdStrike Falcon RTR

## ❓ Questions I Had / Things to Revisit

- Want hands-on time in an actual EDR console (even a free-tier/demo) to
  see a real process tree and alert investigation
- Curious how much manual tuning is needed to keep EDR's ML-based
  detection from generating excess false positives
- Want to map a few more example detections to their MITRE ATT&CK
  Tactic/Technique myself, for practice

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
EDR's three pillars, walk through the AV vs EDR scenario, and describe how
telemetry, agents, and the console work together confidently.

---

*This is one of the most detailed and genuinely exciting rooms so far — the
AV vs EDR attack-chain table makes the value of EDR extremely concrete, and
I can already see how this connects directly to the SIEM room coming up
next, since EDR is one of the key data sources feeding into it.*
