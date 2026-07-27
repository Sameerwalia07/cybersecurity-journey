# TryHackMe — Elastic: The Basics

**Path:** SOC Level 1 — Module 3: Core SOC Solutions
**Date completed:** [16/07/2026]
**Room link:** [https://tryhackme.com/room/investigatingwithelk101]

---

## 🎯 What I Learned

- What the Elastic Stack (ELK) is and why SOC teams use it like a SIEM
  despite not being a traditional one
- The four core components: Elasticsearch, Logstash, Beats, Kibana
- How these components work together end-to-end
- The layout of Kibana's Discover tab
- What index patterns are and why they matter
- KQL (Kibana Query Language) — free text search, wildcards, logical
  operators, and field-based search
- The basics of creating visualisations and dashboards

## 🧠 In My Own Words

The **Elastic Stack (ELK)** was originally built to store, search, and
visualise large volumes of data — first popular for monitoring application
performance, but its capabilities made it increasingly popular in security
operations too. Even though it's **not a traditional SIEM**, many SOC teams
use it almost like one, thanks to its strong search and visualisation
abilities.

ELK is a collection of open-source components working together to collect,
store, search, and visualise data in real time.

### The Four Core Components

**1. Elasticsearch** — a full-text search and analytics engine for
JSON-formatted documents. It stores, analyses, and correlates data, and
exposes a **RESTful API** for interaction.

**2. Logstash** — a data processing engine that ingests data from various
sources, filters/normalises it, then sends it to a destination (Kibana, a
listening port, etc.). A Logstash config file has three parts:
1. **Input** — defines the data source being ingested
2. **Filter** — specifies how to normalise the ingested data
3. **Output** — defines where the filtered data goes (port, Kibana,
   Elasticsearch, file)

Logstash supports a wide range of Input, Output, and Filter plugins.

**3. Beats** — lightweight, host-based **data-shipper agents** that
transfer data from endpoints to Elasticsearch. Each Beat is
single-purpose — e.g. **Winlogbeat** collects Windows event logs,
**Packetbeat** collects network traffic flows.

**4. Kibana** — the web-based visualisation tool that works with
Elasticsearch to analyse, investigate, and visualise data streams in real
time, letting users build dashboards and visualisations for better
visibility.

### How They Work Together

```
Beats (collect from endpoints) 
   → Logstash (parse/normalise into field-value pairs) 
      → Elasticsearch (store/search/analyse) 
         → Kibana (visualise/investigate)
```

### The Kibana Discover Tab — Interface Breakdown

1. **Logs** — each row is a single log event, with its parsed fields and
   values
2. **Fields Pane** — left-side list of parsed fields; click any to add/
   remove it from the active search filter
3. **Index Pattern** — selects which type of log data to view (e.g. a
   dedicated pattern for VPN logs)
4. **Search Bar** — where search queries and filters are entered
5. **Time Filter** — narrows results to a specific time range
6. **Time Interval** — a chart showing event counts over time
7. **Top Bar** — options to save, open, or share searches
8. **Discover Tab** — the main workspace for exploring/searching raw data
9. **Add Filter** — apply filters to specific fields without typing a full
   query manually

### Index Patterns

Kibana requires an **index pattern** to know which Elasticsearch data to
explore — each pattern maps to defined field properties, and a single
pattern can point to multiple indices. Since every log source has a
different structure, logs get normalised into fields/values via a
dedicated index pattern per data source when ingested.

### KQL (Kibana Query Language)

KQL is used to search ingested logs/documents in Elasticsearch, in two main
ways:

**Free text search** — searches by term only, regardless of field:
- `security` → returns all documents containing that exact term
- `United` alone returns **nothing**, since KQL matches whole
  terms/words, not partial ones
- The wildcard `*` allows partial matching: `United*` would match
  "United", "United States," etc.

**Logical operators:**
- **AND** — `"United States" AND "Virginia"` → logs containing both terms
- **OR** — `"United States" OR "England"` → logs containing either term
- **NOT** — `"United States" AND NOT ("Florida")` → US logs excluding
  Florida specifically

**Field-based search** — uses `Field: Value` syntax to search specific
fields directly:
- `Source_ip : 238.163.231.224 AND UserName : Suleman` → logs where
  `Source_ip` matches that exact value **and** `UserName` is "Suleman"

### Creating Visualisations and Dashboards

Kibana lets you turn indexed data into visual elements (bar charts, pie
charts, time-series graphs, data tables, etc.) built directly from a chosen
index pattern and query/filter — similar in spirit to Splunk's
visualisation options. Multiple visualisations can then be combined into a
single **Dashboard**, giving a consolidated, real-time view of key metrics
(e.g. failed logins over time, top source IPs, alert counts) — useful for
both ongoing monitoring and quickly investigating specific data during an
incident.

## 🛠️ Key Terms Introduced

- Elasticsearch, Logstash, Beats, Kibana
- Winlogbeat, Packetbeat
- Index pattern
- KQL: free text search, wildcards, AND/OR/NOT, field-based search
- Visualisations, Dashboards

## ❓ Questions I Had / Things to Revisit

- Want hands-on practice writing several KQL queries myself, especially
  combining field-based search with logical operators
- Curious how ELK's free/open-source nature compares practically to
  Splunk's licensing model for a real SOC team choosing between them
- Want to actually build a simple dashboard with 2-3 visualisations to get
  comfortable with the workflow

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
all four ELK components, how they connect, the Discover tab layout, and
KQL search syntax confidently.

---

*Nice to now have both major SIEM-adjacent tools (Splunk and ELK) covered
back to back — SPL vs KQL are clearly solving the same problem with
different syntax, which should make picking up either one in a real job
much less intimidating.*
