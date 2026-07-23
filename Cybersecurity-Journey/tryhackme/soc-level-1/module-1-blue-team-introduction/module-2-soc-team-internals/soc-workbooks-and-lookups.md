# TryHackMe — SOC Workbooks and Lookups

**Path:** SOC Level 1 — Module 2: SOC Team Internals
**Date completed:** [14/07/2026]
**Room link:** [https://tryhackme.com/room/socworkbookslookups]

---

## 🎯 What I Learned

- What identity inventory and asset inventory are, and why they matter
  during triage
- How to use a network diagram to reconstruct an attack path from raw
  firewall/IP data
- What a SOC workbook is and why L1 analysts rely on them
- The three logical groups a workbook is typically divided into

## 🧠 In My Own Words

Alert triage often requires pulling in **additional context** about the
affected employee or system — this room covers the lookup tools and
workbook structures that make that process faster and more consistent.

**Identity inventory** is a catalogue of corporate employees (user
accounts) and services (machine accounts), along with details like
privileges, contacts, and roles within the company.

**Asset inventory** (or asset lookup) is a list of all computing resources
within an organisation's IT environment.

### Using a Network Diagram to Reconstruct an Attack

Beyond identity/asset context, understanding the **network** layer matters
too, especially at larger companies. Example scenario walked through in the
room:

1. **08:00** — External IP `103.61.240.174` repeatedly connects to the
   corporate firewall on `TCP/10443`
2. **08:23** — That external IP gets translated to an internal IP
   `10.10.0.53`
3. **08:25** — `10.10.0.53` scans the `172.16.15.0/24` range, finds no open
   ports
4. **08:32** — The same IP scans `172.16.23.0/24` — the attack is clearly
   ongoing

A **network diagram** — a visual map of locations, subnets, and their
connections — helps answer the natural questions this raises (what service
runs on port 10443, why this subnet would try reaching others). Using the
diagram, the attack path can be reconstructed as:

1. An attacker behind `103.61.240.174` performed a **VPN brute force**
   against `vpn.tryhatme.thm`
2. After a successful login, they were assigned an IP from the **VPN
   Subnet**
3. They attempted to scan the **Database Subnet**, but were likely blocked
   by firewall rules
4. Having failed there, they pivoted to scanning the **Office Subnet**,
   looking for their next target

This shows how raw, disconnected log entries become a coherent attack
story once mapped against the network's actual structure.

### SOC Workbooks

A **SOC workbook** (also called a playbook, runbook, or workflow) is a
structured document defining the steps to investigate and remediate
specific threats efficiently and consistently. Since L1 analysts are junior
and aren't expected to perfectly handle every possible scenario, senior
analysts often build workbooks to support them. L1 analysts are typically
expected (sometimes required) to follow workbooks precisely, to avoid
mistakes and keep triage consistent.

**A workbook is typically divided into three logical groups:**
1. **Enrichment** — use threat intelligence and identity inventory to
   gather context about the affected user
2. **Investigation** — using the gathered data and SIEM logs, form a
   verdict on whether the activity (e.g. a login) is expected or not
3. **Escalation** — escalate to L2 or communicate directly with the user if
   necessary

Different teams build workbooks differently — some have hundreds of
detailed workbooks per detection rule (closer to a SOAR automation
playbook), while others keep just a handful of high-level workbooks and
lean more on analyst judgement. Either way, an L1 analyst should be able to
break an investigation into modular steps and build simple workbook logic
around it themselves.

## 🛠️ Key Terms Introduced

- Identity inventory
- Asset inventory
- Network diagram
- SOC workbook / playbook / runbook
- Enrichment, Investigation, Escalation (workbook structure)

## ❓ Questions I Had / Things to Revisit

- Want to try building a simple workbook myself for a common scenario (e.g.
  unusual login location) using the Enrichment → Investigation →
  Escalation structure
- Curious what tools are typically used to actually query identity/asset
  inventory in practice (is this usually a dedicated CMDB, or built into
  the SIEM?)
- Want more practice reconstructing attack paths from raw log timestamps,
  like the VPN brute force example here

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
identity/asset inventory, walk through the network diagram attack
reconstruction, and describe workbook structure confidently.

---

*This connects directly back to Alert Triage's "investigation" step —
workbooks are essentially the structured version of that 4-step
recommendation, and identity/asset inventory plus network diagrams are the
lookup tools that fuel the "gather context" part of any triage.*
