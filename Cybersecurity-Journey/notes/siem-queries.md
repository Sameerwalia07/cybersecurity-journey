# SIEM Query Reference — Splunk SPL vs Kibana KQL

Side-by-side syntax reference for the two SIEM query languages covered so
far, since they solve the same problems with different syntax.

## Basic Search

| Task | Splunk (SPL) | Kibana (KQL) |
|---|---|---|
| Search a term | `security` | `security` |
| Field match | `field=value` | `field: value` |
| Wildcard | `United*` | `United*` |

## Logical Operators

| Operator | Splunk (SPL) | Kibana (KQL) |
|---|---|---|
| AND | `"A" AND "B"` | `"A" AND "B"` |
| OR | `"A" OR "B"` | `"A" OR "B"` |
| NOT | `"A" NOT "B"` | `"A" AND NOT "B"` |

## Field-Based Search Examples

**Splunk:**
```spl
index=linux_logs sourcetype=linux_secure "Failed password"
| stats count by src_ip, user
| where count > 5
```
*(Counts failed SSH logins by source IP/user, filters for >5 attempts —
classic brute-force detection query)*

**Kibana (KQL):**
```
Source_ip: 238.163.231.224 AND UserName: Suleman
```
*(Finds logs where both the source IP and username match specific values)*

## Common SPL Commands

```spl
| stats count by field        # count occurrences grouped by a field
| where condition                # filter results by a condition
| sort - field                     # sort descending by a field
| table field1, field2               # display only specific fields
| top field                            # show most common values of a field
```

## Quick Comparison

| | Splunk (SPL) | Kibana (KQL) |
|---|---|---|
| Search bar syntax | SPL (pipe-based) | KQL (simpler, closer to natural language) |
| Best for | Complex stats/aggregation | Fast free-text + field search |
| Ecosystem | Forwarder → Indexer → Search Head | Beats → Logstash → Elasticsearch → Kibana |

## Detection Rule Building Blocks (from SIEM rooms)

To build a detection rule, you generally need:
1. **Log source** (e.g. WinEventLog)
2. **Event ID / EventCode** (e.g. 4688 for process execution)
3. **Specific field/value** to match (e.g. `NewProcessName contains whoami`)
4. **Alert message** to trigger

*Example: "If Log Source = WinEventLog AND EventCode = 4688 AND
NewProcessName contains whoami → Trigger alert 'WHOAMI command Execution
DETECTED'"*

---
*See `detection-rules-cheatsheet.md` for more worked examples of building
actual detection logic on top of these queries.*
