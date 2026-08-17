# Incident Response Cheat Sheet — Frameworks + Report Template

Quick reference for IR frameworks and a ready-to-fill alert report
template, pulled from Incident Response Fundamentals and SOC L1 Alert
Reporting.

## SANS vs NIST — Side by Side

| SANS (PICERL) | NIST |
|---|---|
| 1. Preparation | 1. Preparation |
| 2. Identification | 2. Detection and Analysis |
| 3. Containment | 3. Containment, Eradication, and Recovery |
| 4. Eradication | (combined above) |
| 5. Recovery | (combined above) |
| 6. Lessons Learned | 4. Post-Incident Activity |

**Note:** SANS "Identification" = NIST "Detection and Analysis" — same
core idea, different name.

## Alert Report Template — The Five Ws

Use this for every escalated alert:

```
WHO:    [Which user logged in, ran the command, or downloaded the file?]

WHAT:   [What exact action or event sequence occurred?]

WHEN:   [When did the suspicious activity start and end?]

WHERE:  [Which device, IP, or website was involved?]

WHY:    [Reasoning for the final verdict — the most important W]

VERDICT: [True Positive / False Positive]

ESCALATED: [Yes/No — if yes, to whom and why]
```

## Escalation Checklist — Should This Go to L2?

Escalate if ANY of these are true:
- [ ] Indicates a major cyberattack requiring deeper investigation/DFIR
- [ ] Remediation needed (malware removal, host isolation, password reset)
- [ ] Requires communication with customers/partners/management/law
      enforcement
- [ ] You don't fully understand the alert and need senior input

## Communication Edge Cases — Quick Reference

| Situation | Action |
|---|---|
| L2 unreachable for 30+ min on a critical alert | Escalate chain: L2 → L3 → Manager |
| Validating account compromise with the affected user | Use an alternative contact method (never the breached channel) |
| Overwhelmed by alert volume | Prioritise per workflow, inform L2 of the situation |
| Realise a past alert was misclassified | Flag to L2 immediately — don't sit on it |
| SIEM logs not parsing correctly | Don't skip the alert — investigate what's possible, report the tooling issue |

## Digital Forensics — 4-Stage Methodology

```
Collection → Examination → Analysis → Reporting
```

**Evidence handling essentials:**
- Proper authorization before collecting
- Chain of custody documented at every step
- Write blockers used to prevent modifying original evidence

---
*Use the Five Ws template directly when practicing alert triage — filling
it out for even a hypothetical alert builds real muscle memory for the
format.*
