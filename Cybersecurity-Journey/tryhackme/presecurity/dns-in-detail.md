# TryHackMe — DNS in Detail

**Path:** Pre Security
**Date completed:** [13/05/2026]
**Room link:** [https://tryhackme.com/room/dnsindetail]

---

## 🎯 What I Learned

- What DNS (Domain Name System) is and the problem it solves
- The structure of a domain name: top-level domain, second-level domain, and
  subdomain
- Common DNS record types: A, AAAA, TXT, MX, CNAME
- The full step-by-step path a DNS request takes, from root servers to the
  final destination

## 🧠 In My Own Words

DNS exists so humans don't have to memorise IP addresses to reach devices on
a network — instead of typing a string of numbers, we type a domain name and
DNS handles translating that into the actual IP address behind the scenes.

**Domain structure** breaks down into parts:
- **Top-Level Domain (TLD):** the last part, like `.com`, `.org`, `.net`
- **Second-Level Domain (SLD):** the main name registered, e.g. `google` in
  `google.com`
- **Subdomain:** an optional prefix before that, e.g. `mail` in
  `mail.google.com`

**Record types** each serve a different purpose:
- **A record:** maps a domain name to an **IPv4** address
- **AAAA record:** maps a domain name to an **IPv6** address
- **CNAME record:** points one domain name to another domain name (an alias),
  rather than directly to an IP
- **MX record:** specifies the mail server responsible for receiving email
  for that domain
- **TXT record:** stores arbitrary text data for a domain — often used for
  verification or security purposes (like SPF records for email)

**How a DNS request actually resolves**, step by step:
1. The request first goes to a **root server**, which doesn't know the exact
   answer but knows which server handles the TLD (e.g. `.com`)
2. It's forwarded to the **TLD server**, which doesn't have the final IP
   either, but knows which server is authoritative for that specific domain
3. It's forwarded to the **authoritative server** for that domain, which
   actually holds the correct DNS records and returns the real answer
4. That answer (usually an IP address) is passed back down the chain until
   it reaches the device that made the original request, which can now
   connect directly to the destination

## 🛠️ Key Terms Introduced

- Top-Level Domain (TLD), Second-Level Domain (SLD), Subdomain
- A, AAAA, CNAME, MX, TXT records
- Root server, TLD server, Authoritative server

## ❓ Questions I Had / Things to Revisit

- Want to understand where **caching and TTL (Time To Live)** fit into this
  process — does every request really go all the way to the authoritative
  server every time, or does a resolver cache the answer?
- Curious how DNS gets **abused** in real attacks (e.g. DNS tunneling, cache
  poisoning) since I know this is a big topic in blue team work later

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through the domain structure, the main record types, and the resolution path
from root to authoritative server confidently.

---

*DNS logs are something SOC analysts look at constantly, so I want to come
back to this room's concepts when I start working with actual DNS logs in a
home lab later.*
