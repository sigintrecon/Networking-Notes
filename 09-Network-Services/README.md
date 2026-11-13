# Module 09 — Network Services

## Learning Objectives

- Explain DNS and the resolution process
- Know common DNS record types
- Describe DHCP and the DORA process
- Explain ICMP, ping, and traceroute
- Understand NAT and PAT

---

## DNS — Domain Name System

DNS translates human-readable names to IP addresses.

You type `google.com`. DNS returns `142.250.80.46`.

### DNS Resolution Process

```
Browser → Recursive Resolver → Root Server → TLD Server → Authoritative Server → IP
```

### Common DNS Record Types

| Record | Purpose |
|--------|---------|
| A | IPv4 address |
| AAAA | IPv6 address |
| MX | Mail server |
| CNAME | Alias (www → actual hostname) |
| NS | Nameserver |
| TXT | Text / verification |
| PTR | Reverse lookup (IP → hostname) |

---

## DHCP — Dynamic Host Configuration Protocol

DHCP automatically assigns IP configuration to devices.

### DORA Process

```
Client          DHCP Server
  │── DISCOVER ──→│  "Is there a DHCP server?"
  │←── OFFER ─────│  "Yes. I offer 192.168.1.50"
  │── REQUEST ────→│  "I'll take 192.168.1.50"
  │←── ACK ────────│  "Confirmed. Lease granted."
```

DHCP assigns: IP address, subnet mask, default gateway, DNS server.

---

## ICMP — Internet Control Message Protocol

Used for diagnostics and error reporting, not data transfer.

```bash
ping 8.8.8.8          # Test reachability
traceroute 8.8.8.8    # Linux — trace path
tracert 8.8.8.8       # Windows — trace path
```

Each router along the path decrements the TTL by 1. When TTL reaches 0, the router sends an ICMP Time Exceeded message — revealing its IP address.

---

## NAT and PAT

NAT allows many devices with private IPs to share one public IP.

```
192.168.1.10 ──→ [Router NAT] ──→ 203.0.113.1 (public)
192.168.1.11 ──→ [Router NAT] ──→ 203.0.113.1 (same public IP)
```

PAT extends NAT using port numbers to track which internal device each connection belongs to. This is what your home router does.

---

## Cybersecurity Relevance

- DNS is a major attack surface: DNS poisoning, DNS tunneling, subdomain enumeration
- DHCP starvation floods the server to exhaust the IP pool
- ICMP can be blocked by firewalls — ping failing does not always mean host is down
- NAT hides internal network structure

---

## Quick Revision

1. DNS = name to IP translation
2. DHCP DORA = Discover, Offer, Request, Acknowledge
3. ICMP = diagnostics (ping, traceroute)
4. NAT/PAT = many private IPs share one public IP using ports
5. DNS record A = IPv4, AAAA = IPv6, MX = mail

---

## Practice Questions

1. What record type maps a domain to an IPv4 address?
2. What are the four steps of the DORA process?
3. What does TTL do in a traceroute?
4. If `ping 8.8.8.8` works but `ping google.com` fails, what is the likely problem?
5. What is the difference between NAT and PAT?
