# SIEM Query Reference — Splunk SPL vs Kibana KQL

Side-by-side syntax reference for the two SIEM query languages covered so
far, since they solve the same problems with different syntax. Updated with
`stats`/`table` patterns for exfiltration and network hunting.

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

## Aggregation Patterns (`stats` + `table`)

`stats` turns many raw events into one row per group. `table` then shows
just the columns I care about. These are the two commands I reach for most
in triage.

**Total bytes sent out per source IP (exfiltration hunting):**
```spl
index=proxy_logs
| stats sum(bytes_out) as total_bytes by src_ip, dest_domain
| sort - total_bytes
| table src_ip, dest_domain, total_bytes
```

**Many small uploads to one destination (low-and-slow exfil):**
```spl
index=proxy_logs http_method=POST
| stats count, sum(bytes_out) as total_bytes by src_ip, dest_domain
| where count > 50
| sort - count
```

**Long DNS hostnames (possible DNS tunnelling):**
```spl
index=dns_logs
| eval name_len=len(query)
| where name_len > 50
| stats count, avg(name_len) as avg_len by src_ip, query
| sort - count
```

**Top talkers by destination port (vertical vs horizontal scan hint):**
```spl
index=firewall_logs action=blocked
| stats dc(dest_port) as unique_ports, dc(dest_ip) as unique_hosts by src_ip
| sort - unique_ports
| table src_ip, unique_ports, unique_hosts
```
*(High `unique_ports` on few hosts = vertical scan; high `unique_hosts` on one
port = horizontal sweep.)*

**Pattern to remember:**
```
search (filter) → stats (aggregate by field) → where (threshold) → sort → table (show)
```

> ⚠️ Index, sourcetype and field names (`proxy_logs`, `bytes_out`,
> `dest_domain`, `query`, etc.) are **placeholders**. In a real SIEM, check
> the actual field names first (the fields sidebar in Splunk, or Discover in
> Kibana) and adjust.

## Extra SPL Commands

```spl
| dc(field)                  # distinct count (inside stats)
| eval new=len(field)        # create a calculated field
| rare field                 # least common values (good for odd domains/processes)
| dedup field                # remove duplicate values
| timechart count by field   # trend over time
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
