# TryHackMe — SOC L1 Alert Reporting

**Path:** SOC Level 1 — Module 2: SOC Team Internals
**Date completed:** [13/07/2026]
**Room link:** [https://tryhackme.com/room/socl1alertreporting]

---

## 🎯 What I Learned

- The overall alert lifecycle from L1 to L2
- The three key concepts: reporting, escalation, and communication
- Why alert reports matter and what purpose they serve
- The Five Ws report format
- When to escalate an alert, and the actual escalation steps
- How to handle tricky real-world communication scenarios

## 🧠 In My Own Words

L1 analysts first receive alerts through a SIEM, EDR, or ticket management
platform. Most get closed as **False Positives** or handled directly at L1,
but complex/threatening ones get passed to **L2**, who handle most actual
remediation. To move an alert forward properly, three concepts matter:
**reporting, escalation, and communication.**

### Alert Reporting

Before closing or escalating an alert, it often needs to be documented —
not just a short comment, but (depending on severity and team standards) a
detailed investigation write-up with all relevant evidence included. This
matters most for **True Positives**, which require escalation.

**Why alert reports matter:**

| Purpose | Explanation |
|---|---|
| **Provide context for escalation** | Saves L2 analysts significant time and helps them understand the situation quickly |
| **Save findings for the record** | Raw SIEM logs are only kept 3-12 months, but alerts are kept indefinitely — so context needs to live in the alert itself |
| **Improve investigation skills** | If you can't explain something simply, you don't fully understand it — writing reports sharpens L1 skills |

**Report format — the Five Ws:**
- **Who:** which user logged in, ran the command, or downloaded the file
- **What:** the exact action or event sequence performed
- **When:** exactly when the suspicious activity started and ended
- **Where:** which device, IP, or website was involved
- **Why:** the most important W — the reasoning behind the final verdict

### Alert Escalation

After forming a verdict and writing the report, the analyst decides whether
to escalate to L2. General recommendations for when to escalate:
1. The alert indicates a major cyberattack requiring deeper
   investigation or DFIR
2. Remediation actions are needed (malware removal, host isolation,
   password reset)
3. Communication with customers, partners, management, or law enforcement
   is required
4. The analyst doesn't fully understand the alert and needs senior help

**Escalation steps (typical SOC dashboard workflow):**
1. Move the alert to **In Progress** and perform the analysis
2. Write an alert report and set a verdict (e.g. True Positive)
3. If escalation is required, assign the alert to the L2 on shift
4. L2 receives a notification and starts from the submitted report

It's noted as completely acceptable — even encouraged, especially early on
— for an L1 analyst to request L2 support rather than closing an alert they
don't fully understand.

### Communication

Beyond L1↔L2 handoffs, analysts often need to communicate with other
departments — e.g. asking IT to confirm granting admin privileges, or
contacting HR about a newly hired employee.

### Handling Real-World Communication Scenarios

Ideally a SOC has formal **Crisis Communication** procedures, but if not,
here's how to handle common tricky situations:

- **L2 unavailable during a critical alert (30+ min no response):** escalate
  the chain — try L2, then L3, then the manager
- **Validating a Slack/Teams account compromise with the affected user:**
  never contact them through the potentially breached chat — use an
  alternative method like a phone call
- **Overwhelming volume of alerts, some critical:** prioritise per the
  normal workflow, but inform the L2 on shift about the situation
- **Realising a past alert was misclassified/missed:** immediately flag it
  to L2 — threat actors can stay silent for weeks before causing real
  impact
- **SIEM logs not parsing/searchable correctly:** don't skip the alert —
  investigate what's possible and report the tooling issue to L2 or a SOC
  engineer

## 🛠️ Key Terms Introduced

- Alert reporting, escalation, communication
- The Five Ws report format
- Crisis Communication procedures

## ❓ Questions I Had / Things to Revisit

- Want to practice writing an actual Five Ws report against a sample alert
  to get the format down naturally
- Curious how much variation exists between teams on "formal escalation
  request" vs a simple reassignment + chat ping
- Want to think through a couple more edge-case scenarios myself, to build
  intuition beyond just the ones listed here

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
the reporting purpose, the Five Ws format, escalation criteria/steps, and
how to handle the communication edge cases confidently.

---

*This pairs directly with Alert Triage — that room taught how to
investigate an alert, this one teaches what to do once you've reached a
verdict. Together they cover the full lifecycle of a single alert from
first look to handoff.*
