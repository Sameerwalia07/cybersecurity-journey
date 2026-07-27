# TryHackMe — Splunk: The Basics

**Path:** SOC Level 1 — Module 3: Core SOC Solutions
**Date completed:** [16/07/2026]
**Room link:** [https://tryhackme.com/room/splunk101]

---

## 🎯 What I Learned

- What Splunk is and its role as a leading SIEM solution
- Splunk's three core components: Forwarder, Indexer, Search Head
- What data each component handles and how they work together
- The layout of the Splunk interface (Splunk Bar, Apps Panel, Explore
  Splunk, Home Dashboard)

## 🧠 In My Own Words

**Splunk** is one of the leading SIEM solutions on the market, allowing
users to collect, analyse, and correlate network and machine logs in real
time. It's built around three main components that work together: the
**Forwarder**, the **Indexer**, and the **Search Head**.

### Splunk Forwarder

A lightweight agent installed on the endpoint being monitored. Its job is
simply to **collect data and send it to the Splunk instance**, using
minimal resources so it doesn't impact the endpoint's performance.

**Key data sources it can pull from:**
- Web servers generating web traffic
- Windows machines generating Event Logs, PowerShell, and Sysmon data
- Linux hosts generating host-centric logs
- Databases generating connection requests, responses, and errors

### Splunk Indexer

Handles the heavy lifting: **processing** data received from forwarders.
It parses and normalises raw data into **field-value pairs**, categorises
it, and stores the results as searchable **events** — making all of it
easy to search and analyse later.

### Splunk Search Head

The actual interface (within the **Search & Reporting** app) where users
search indexed logs, using **SPL (Search Processing Language)** — Splunk's
powerful query language. When a search is run, the request goes to the
indexer, which returns the relevant events as field-value pairs. The Search
Head also lets you transform raw results into **tables and visualisations**
like pie, bar, and column charts.

### How the Three Components Fit Together

```
Endpoint → Forwarder (collects) → Indexer (processes/stores) → Search Head (search/visualise)
```

Each component has one clear job, which makes the overall pipeline easy to
reason about: collect → process → search.

### Navigating the Splunk Interface

**Splunk Bar** (top panel):
- **Messages** — system-level notifications
- **Settings** — configure the Splunk instance
- **Activity** — track progress of search jobs/processes
- **Help** — tutorials and documentation
- **Find** — search across the whole app

**Apps Panel** — shows installed apps for the instance; every Splunk
install comes with the default **Search & Reporting** app.

**Explore Splunk** — quick links to add data, add new apps, and access
documentation.

**Home Dashboard** — no dashboards shown by default, but a range of
built-in dashboards are available via a dropdown or the dashboards listing
page.

## 🛠️ Key Terms Introduced

- Splunk Forwarder, Indexer, Search Head
- SPL (Search Processing Language)
- Field-value pairs, Events
- Splunk Bar, Apps Panel, Explore Splunk, Home Dashboard

## ❓ Questions I Had / Things to Revisit

- Want hands-on practice writing actual SPL queries — this room covered the
  interface but I haven't built a real search yet
- Curious how forwarders are actually configured/deployed at scale across
  many endpoints in a real company
- Want to explore what a few of the default built-in dashboards actually
  show, rather than just knowing they exist

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
the three-component pipeline and the basic interface layout confidently.
SPL query-writing is the clear next hands-on skill to build.

---

*This makes the earlier SIEM theory concrete — "log ingestion via
agent/forwarder" and "normalization" from the Introduction to SIEM room are
literally the Forwarder and Indexer here. Ready to start actually
searching logs with SPL next.*
