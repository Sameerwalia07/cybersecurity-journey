# TryHackMe — Incident Response Fundamentals

**Path:** Cyber Security 101
**Date completed:** [16/06/2026]
**Room link:** https://tryhackme.com/room/incidentresponsefundamentals

---

## 🎯 What I Learned

- What a cyber security incident is, and the real-world scale of these events
- The difference between false positives and true positives, and severity
  levels
- Common types of incidents
- Two major incident response frameworks: SANS (PICERL) and NIST
- Security solutions that support detection and response: SIEM, AV, EDR
- The difference between Playbooks and Runbooks

## 🧠 In My Own Words

A **cyber security incident** is essentially any cyber attack on an
organisation that causes real damage — often financial, sometimes reported
as losses of thousands of dollars, and these happen daily across the
internet. **Incident Response (IR)** is the discipline that handles an
incident from **start to end** — this includes deploying security measures
to prevent incidents in the first place, actively responding when one
occurs, and minimising its overall impact. It's a thorough, structured
guideline rather than a single reactive action.

Two important concepts when reviewing alerts:
- **False positive** — an alert that looks like an incident but isn't
  actually malicious
- **True positive** — an alert that correctly identifies a real incident

Incidents are also assigned **severity levels**, helping teams prioritise
which ones need urgent attention.

**Common types of incidents:**
- Malware infections
- Data breaches
- Insider attacks
- Denial of Service (DoS) attacks

**Two major IR frameworks:**

**SANS — PICERL** (6 phases):
1. **P**reparation
2. **I**dentification
3. **C**ontainment
4. **E**radication
5. **R**ecovery
6. **L**essons Learned

**NIST** (4 phases):
1. Preparation
2. Detection and Analysis
3. Containment, Eradication, and Recovery
4. Post-Incident Activity

Interestingly, SANS's "Identification" phase and NIST's "Detection and
Analysis" phase cover the same core idea — this is the stage where you
actually recognise that an incident is happening. Since manually spotting
abnormal behaviour is extremely difficult at scale, several security
solutions exist to help detect (and sometimes even respond to) incidents:

- **SIEM (Security Information and Event Management):** collects logs from
  across an environment into one centralised location and correlates them
  to help identify incidents
- **AV (Antivirus):** detects known malicious programs and regularly scans
  systems for them
- **EDR (Endpoint Detection and Response):** deployed on individual systems,
  protecting against more advanced threats — and unlike AV, EDR can often
  also **contain and eradicate** the threat itself, not just detect it

The **formal incident response document** an organisation maintains is
called the **Incident Response Plan**. Within that broader plan:
- **Playbooks** — step-by-step instructions for how to handle a *specific
  kind* of incident (e.g. a ransomware playbook, a phishing playbook),
  saving significant time during a real event
- **Runbooks** — more granular than playbooks; the actual detailed,
  step-by-step execution of specific tasks during an incident, which can
  vary depending on the tools/resources available to the investigating team

## 🛠️ Key Terms Introduced

- False positive / True positive
- Severity levels
- SANS PICERL framework
- NIST IR framework
- SIEM, AV, EDR
- Incident Response Plan
- Playbook vs Runbook

## ❓ Questions I Had / Things to Revisit

- Want to see a real example playbook (e.g. for phishing or ransomware) to
  understand how detailed they typically are
- Curious how SANS vs NIST frameworks are chosen by different organisations
  — is one more common in certain industries?
- Want to understand EDR's containment/eradication capability more
  concretely — what does "containing" a threat actually look like from the
  EDR console?

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
both frameworks, the tools involved in detection, and the
playbook/runbook distinction confidently.

---

*This ties directly into SOC Fundamentals and Digital Forensics — SOC
triage identifies the incident, this framework guides the structured
response, and forensics kicks in for the deeper investigation. Starting to
see how these rooms form one connected picture of the full incident
lifecycle.*
