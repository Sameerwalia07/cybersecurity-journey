# TryHackMe — SOC Metrics and Objectives

**Path:** SOC Level 1 — Module 2: SOC Team Internals
**Date completed:** [14/07/2026]
**Room link:** [https://tryhackme.com/room/socmetricsobjectives]

---

## 🎯 What I Learned

- The core alert-based metrics: Alerts Count, False Positive Rate, Alert
  Escalation Rate, Threat Detection Rate
- The time-based metrics tied to SLAs: MTTD, MTTA, MTTR
- What "good" looks like for each metric, and why
- Practical steps to improve each metric when it's underperforming

## 🧠 In My Own Words

Like any department, a SOC team's efficiency can be measured with specific
metrics. The SOC's overall goal is protecting the **confidentiality,
integrity, and availability** of an organisation's digital assets, achieved
by developing, receiving, and triaging alerts — with L1's specific job
being to reliably report True Positives up to L2.

### The Four Core Alert Metrics

| Metric | Formula | Measures |
|---|---|---|
| **Alerts Count (AC)** | Total alerts received | Overall analyst workload |
| **False Positive Rate (FPR)** | False Positives ÷ Total Alerts | Level of noise in alerts |
| **Alert Escalation Rate (AER)** | Escalated Alerts ÷ Total Alerts | Experience/independence of L1 analysts |
| **Threat Detection Rate (TDR)** | Detected Threats ÷ Total Threats | Overall reliability of the SOC team |

**Alerts Count** — 80 unresolved alerts at shift start is overwhelming and
risks missing real threats in the noise. But a whole week with *zero*
alerts is also concerning — it may signal a SIEM issue or a visibility gap
rather than genuine safety. A healthy range is generally **5-30 alerts per
day per L1 analyst**, depending on company size.

**False Positive Rate** — if 94% of alerts turn out to be noise, analysts
naturally become less vigilant and start treating everything as "just
spam" — which is exactly how real threats get missed. **0% is unrealistic**,
but **80%+ is a serious problem**, usually fixed through detection rule
tuning ("False Positive Remediation").

**Alert Escalation Rate** — L2 relies on L1 to filter noise and escalate
only genuinely actionable alerts. But L1 shouldn't be overconfident either,
triaging things they don't fully understand without senior input. Target is
generally **below 50%, ideally below 20%**.

**Threat Detection Rate** — example: out of 6 real attacks in a year, the
SOC caught 4, missed one due to a broken detection rule, and misclassified
another as a False Positive → **TDR = 4/6 = 67%**, a bad result. TDR should
always aim for **100%**, since every missed threat can lead to devastating
consequences like ransomware or data exfiltration.

### SLA-Based Time Metrics

An alert alone doesn't stop a breach — timely receipt, triage, and response
matter just as much. These requirements are usually formalised in a
**Service Level Agreement (SLA)** — a document between the SOC team and
company management (or between an MSSP and its customers). Key elements:

- **SOC Team Availability** — the team's working schedule, e.g. Mon-Fri
  (8/5) or full 24/7 coverage
- **MTTD (Mean Time to Detect)** — average time between the attack
  occurring and the SOC detecting it
- **MTTA (Mean Time to Acknowledge)** — average time for L1 to start
  triaging a new alert
- **MTTR (Mean Time to Respond)** — average time taken to actually stop the
  breach from spreading

### Improving Each Metric

| Metric | Threshold | Improvement Actions |
|---|---|---|
| **False Positive Rate** | Over 80% | Exclude trusted activity (e.g. system updates) from detection rules; automate common alert triage via SOAR or scripts |
| **Mean Time to Detect** | Over 30 min | Ask SOC engineers to speed up/increase detection rule frequency; verify SIEM logs are ingested in real time, not delayed |
| **Mean Time to Acknowledge** | Over 30 min | Ensure real-time analyst notifications; distribute alerts evenly across the shift's analysts |
| **Mean Time to Respond** | Over 4 hours | As L1, escalate threats to L2 as quickly as possible; make sure documented playbooks exist for common attack scenarios |

## 🛠️ Key Terms Introduced

- Alerts Count, False Positive Rate, Alert Escalation Rate, Threat
  Detection Rate
- SLA (Service Level Agreement)
- MTTD, MTTA, MTTR
- SOC Team Availability

## ❓ Questions I Had / Things to Revisit

- Want to see what a real SOC dashboard tracking these metrics actually
  looks like
- Curious how these metrics get reported upward — is this something the
  SOC Manager compiles weekly/monthly for leadership?
- Want to understand better how MTTD is even measured when the "attack
  start time" isn't always obvious after the fact

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
all four alert-based metrics and the three SLA time metrics, along with
what healthy thresholds look like and how to improve each one.

---

*This gives real numbers to aim for as I build my own home lab and
eventually work real alerts — knowing "5-30 alerts/day" and "TDR should be
100%" turns abstract SOC concepts into concrete targets I can actually
measure myself against later.*
