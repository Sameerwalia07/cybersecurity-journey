# TryHackMe — SOC L1 Alert Triage

**Path:** SOC Level 1 — Module 2: SOC Team Internals
**Date completed:** [13/07/2026]
**Room link:** [https://tryhackme.com/room/socl1alerttriage]

---

## 🎯 What I Learned

- How a raw event becomes an alert
- The platforms used to manage alerts
- How responsibility for triage is spread across the SOC team
- The core properties every alert has
- How to prioritise alerts when facing a full queue
- The initial actions and investigation approach for handling an alert

## 🧠 In My Own Words

Knowing how to properly handle an **alert** is one of the most important
SOC skills — it ultimately decides whether a breach gets detected and
stopped, or missed entirely.

### From Events to Alerts

The pipeline works like this:
1. An **event** occurs (user login, process launch, file download, etc.)
2. The relevant system (OS, firewall, cloud provider) **logs** that event
3. All logs get shipped to a security solution like **SIEM** or **EDR**
4. Since a SOC can receive **millions of logs per day**, an **alert** — a
   notification generated when a specific event or sequence matches a
   detection rule — highlights only the suspicious, anomalous events

This is what makes the job possible: instead of manually reviewing millions
of raw logs, analysts triage just **dozens of alerts per day**.

### Alert Management Platforms

| Solution | Examples | Description |
|---|---|---|
| **SIEM** | Splunk ES, Elastic | Solid built-in alert management, a strong default choice for most SOC teams |
| **EDR / NDR** | MS Defender, CrowdStrike | Have their own alert dashboards, but SIEM/SOAR is usually preferred for centralised triage |
| **SOAR** | Splunk SOAR, Cortex SOAR | Used by bigger SOC teams to aggregate and centralise alerts across multiple solutions |
| **ITSM** | Jira, TheHive | Some teams use dedicated ticket management systems for alert/case tracking |

### L1's Role in Alert Triage

L1 analysts are the **first line of defence** and work with alerts the
most — anywhere from zero to a hundred alerts a day, any one of which could
reveal a real attack. But the whole SOC team plays a part:
- **L1 Analysts** — review alerts, separate real threats from noise, escalate confirmed threats to L2
- **L2 Analysts** — receive escalated alerts, perform deeper analysis and remediation
- **SOC Engineers** — ensure alerts contain enough information for efficient triage
- **SOC Manager** — tracks the speed and quality of triage to make sure real attacks aren't missed

### Core Alert Properties

| Property | Description | Example |
|---|---|---|
| **Alert Time** | When the alert was created (usually a few minutes after the actual event) | Alert Time: 15:35 / Event Time: 15:32 |
| **Alert Name** | Summary based on the detection rule that fired | "Unusual Login Location," "Windows RDP Bruteforce" |
| **Alert Severity** | Urgency level, set by detection engineers, adjustable by analysts | Low, Medium, High, Critical |
| **Alert Status** | Whether someone is actively working the alert | New, In Progress, Closed |
| **Alert Verdict** | Whether the alert turned out to be real or noise | True Positive vs False Positive |
| **Alert Assignee** | The analyst who owns/reviews the alert | Assignee can sometimes be called alert owner |
| **Alert Description** | Explains the rule's logic, why it may indicate an attack, and sometimes how to triage it | The logic of the alert generating rule |
| **Alert Fields** | Specific values that triggered the alert | Affected hostname, entered command line |

### Alert Prioritisation

With hundreds of alerts in a queue, deciding what to pick up first —
**alert prioritisation** — is critical for timely detection. A common,
generic approach:
1. **Filter** — only take new, unseen, unresolved alerts (don't duplicate
   work already being handled by a teammate)
2. **Sort by severity** — Critical first, then High, Medium, Low, since
   detection engineers design rules so critical alerts are far more likely
   to represent real, high-impact threats
3. **Sort by time** — oldest first, since an older breach likely means the
   attacker has had more time to progress (e.g. already exfiltrating data),
   while a newer one may still be in early discovery

### Handling an Alert: Initial Actions and Investigation

**Initial actions** — take ownership before digging in:
1. Assign the alert to yourself
2. Move its status to "In Progress"
3. Familiarise yourself with the alert's name, description, and key
   indicators before proceeding

**Investigation** — the most complex step, requiring technical judgement to
assess legitimacy using SIEM/EDR logs. Some teams provide **Workbooks**
(also called playbooks/runbooks) with step-by-step guidance for specific
alert categories. Without one, general recommendations are:
1. Identify who/what is under threat (user, hostname, cloud resource, etc.)
2. Note the specific action described in the alert (suspicious login,
   malware, phishing, etc.)
3. Review surrounding events for suspicious activity shortly before/after
   the alert
4. Use threat intelligence platforms or other resources to verify your
   findings

## 🛠️ Key Terms Introduced

- Event vs Alert
- SIEM, EDR, NDR, SOAR, ITSM
- Alert properties: Time, Name, Severity, Status, Verdict, Assignee,
  Description, Fields
- Alert prioritisation
- True Positive / False Positive
- Workbooks / Playbooks / Runbooks

## ❓ Questions I Had / Things to Revisit

- Want to see a real alert dashboard (e.g. in Splunk) to connect these
  properties to an actual interface rather than just a table
- Curious how severity gets initially calibrated by detection engineers —
  what makes a rule "Critical" vs "Medium" by design?
- Want hands-on practice actually triaging a sample alert start to finish,
  applying the 4-step investigation approach

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
the event-to-alert pipeline, alert properties, prioritisation logic, and
the initial-action-then-investigation workflow confidently.

---

*This is probably the single most practically important room so far for
the actual day-to-day of an L1 role — everything from properties to
prioritisation feels like something I'll be doing literally every single
shift once I'm in the role.*
