# Web Attack Log Analysis Checklist

A reusable checklist for investigating web server logs, built from Web
Security Essentials, Detecting Web Attacks, Detecting Web Shells and
Detecting Web DDoS (Module 8).

## 1. Know the Log Fields

```
client_ip  - [timestamp]  "METHOD /path?query HTTP/1.1"  status  size  "referrer"  "user-agent"
```

| Field | Suspicious when |
|---|---|
| Client IP | Known-bad, outside expected geography, or one IP with huge volume |
| Timestamp | Odd hours, many requests per second (bursts) |
| Method | `PUT`, `DELETE`, `OPTIONS`, `HEAD` where not expected; `POST` to upload paths |
| Path | `/admin`, `/backup`, `/uploads/*.php`, `.jsp`, `.aspx` in upload folders |
| Query string | `cmd=`, `exec=`, SQL syntax (`' OR '1'='1`), Base64 or URL-encoded values, very long strings |
| Status | Run of `404`s then `200`s (fuzzing); `302` after many failed `POST`s (brute-force success); spike of `5xx` (DoS impact) |
| Size | Much smaller or larger than normal for that page |
| Referrer | Missing or doesn't fit normal navigation (not conclusive alone) |
| User-Agent | `sqlmap`, `wpscan`, `curl`, `wget`, `python-requests`, `Python-urllib`, `ffuf`, ancient browsers (MSIE 6.0), truncated `Mozilla/4.0` |

*Remember: access logs usually **don't record POST bodies**. For credentials or
payloads, go to a packet capture or application logs.*

## 2. Attack Pattern Cheat Sheet

| Attack | Pattern in logs | Confirm with |
|---|---|---|
| **Directory fuzzing / recon** | One IP, many different paths, mostly `404`, a few `200` | Tool User-Agent, burst timing |
| **Brute force** | Many `POST /login` from one IP (or spread out), then `302`/different size | Failed-login events, auth logs |
| **SQL injection** | SQL keywords/quotes in query strings, sqlmap User-Agent, odd response sizes | WAF logs, PCAP (POST bodies), DB error logs |
| **Command injection** | `;`, `|`, `&&`, `whoami`, `cat /etc/passwd` in parameters | Process creation logs (web server spawning shell) |
| **XSS** | `<script>`, `onerror=`, encoded variants in parameters | Client-side: hard from logs, check the injection request |
| **Web shell** | Upload (`POST`/`PUT`), then repeated hits on one new file with `cmd=`/`exec=` | Auditd (`creat`/`execve`), file system search, PCAP |
| **DoS / DDoS** | High request rate to heavy endpoints (`/login`, `/search`, `/checkout`), `503` spike, random query strings on cached URLs | CDN/WAF dashboard, SIEM timechart |

## 3. Triage Steps

1. **Scope:** which host/site, which time window?
2. **Pivot on the suspicious IP:** everything it requested, in order
3. **Check the sequence:** recon → exploit → access → follow-up (map to the Kill Chain)
4. **Check outcomes:** status codes and response sizes, did it work?
5. **Correlate:** WAF, auditd, EDR/Sysmon, DNS and proxy logs, PCAP if available
6. **Check the host:** new/modified files, web server spawning shells, new accounts
7. **Decide:** true positive, false positive or benign? Document the Five Ws
8. **Escalate/contain** per the playbook: block IP, isolate host, preserve evidence

## 4. Handy Commands (illustrative)

**Linux (Apache/Nginx logs):**
```bash
# Top IPs by request count
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head

# Requests per status code
awk '{print $9}' access.log | sort | uniq -c | sort -nr

# Everything one IP did
grep "203.0.113.55" access.log

# Hits on login page
grep "POST /login" access.log | awk '{print $1}' | sort | uniq -c | sort -nr

# Known tool User-Agents
grep -iE "sqlmap|wpscan|nikto|curl|wget|python" access.log

# Recently modified PHP files
find /var/www -name "*.php" -newerct "2025-08-01"

# Dangerous functions in web content
grep -rnE "eval\(|shell_exec\(|passthru\(|system\(" /var/www/html
```

**Splunk (placeholder field names):**
```spl
index=web_logs | stats count by src_ip | sort - count
index=web_logs status=404 | stats count by src_ip | where count > 50
index=web_logs uri_path="/login*" method=POST | stats count by src_ip | where count > 20
index=web_logs | timechart span=1m count by uri_path
```

**Wireshark:**
```
http.request.method == "POST"
http.request.uri contains ".php"
http.user_agent contains "sqlmap"
http.response.code == 503
```

## 5. WAF / Mitigation Ideas

- Block known tool User-Agents (easy to evade, so don't rely on it alone)
- **Rate limit** sensitive endpoints (e.g. `/login` 5 per minute per IP)
- CAPTCHA/JS challenge for suspicious traffic
- Geo/IP reputation blocking and threat-intel feeds
- Validate and sanitise input; parameterised queries
- Validate uploads (type, extension, content), store outside the web root, no script execution in upload folders
- Patch web servers and dependencies

---
*Pairs with `detection-rules-cheatsheet.md` (rules) and `siem-queries.md`
(queries). When a new web room adds an indicator, add it to the tables above.*
