# Networking Tools — Nmap, Wireshark, Tcpdump Reference

A practical syntax cheat sheet for the three main networking/traffic
analysis tools covered so far.

## Nmap — Network Scanning

```bash
nmap 192.168.1.1                    # basic scan of a single host
nmap 192.168.1.0/24                   # scan an entire subnet
nmap -sV 192.168.1.1                    # detect service versions
nmap -sС 192.168.1.1                      # run default scripts
nmap -p 1-1000 192.168.1.1                  # scan a specific port range
nmap -p- 192.168.1.1                          # scan all 65535 ports
nmap -O 192.168.1.1                             # attempt OS detection
nmap -A 192.168.1.1                               # aggressive scan (OS, version, scripts, traceroute)
```

## Wireshark — Display Filters

```
ip.addr == 192.168.1.1          # traffic to/from a specific IP
tcp.port == 443                   # traffic on a specific port
http.request                        # only HTTP requests
dns                                   # only DNS traffic
tcp.flags.syn == 1 && tcp.flags.ack == 0   # only SYN packets (scan detection)
http.request.method == "POST"        # only HTTP POST requests
```

**Useful right-click actions:**
- **Follow → TCP Stream** — reconstruct a full conversation
- **Apply as Filter** — instantly build a filter from a selected field

## Tcpdump — Command-Line Packet Capture

```bash
tcpdump -i eth0                       # capture on interface eth0
tcpdump -i eth0 port 80                 # capture only port 80 traffic
tcpdump -i eth0 host 192.168.1.1          # capture traffic to/from an IP
tcpdump -i eth0 -w capture.pcap             # write capture to a file
tcpdump -r capture.pcap                       # read a saved capture file
tcpdump -i eth0 -c 100                          # capture only 100 packets
```

## Quick Comparison

| Tool | Best For |
|---|---|
| **Nmap** | Discovering hosts/services/open ports on a network |
| **Wireshark** | Deep, visual packet-by-packet analysis (GUI) |
| **Tcpdump** | Quick packet capture on servers without a GUI |

## Quick Examples

```bash
# Find all live hosts on a subnet, then scan the interesting ones
nmap -sn 192.168.1.0/24
nmap -sV -p- 192.168.1.50

# Capture only suspicious outbound traffic on a non-standard port
tcpdump -i eth0 dst port 4444 -w suspicious.pcap
```

---
*Wireshark filters and Nmap flags are the two things worth having memorised
cold — they come up in nearly every hands-on networking/investigation
room.*
