# Nmap Basics

Nmap discovers hosts and scans for open ports.

**Only scan systems you own or have explicit written authorization to scan. Unauthorized scanning is illegal.**

---

## Basic Syntax

```
nmap [options] [target]
```

Target examples:
- Single IP: `192.168.1.1`
- Range: `192.168.1.1-254`
- Subnet: `192.168.1.0/24`

---

## Common Scan Types

| Command | Type | Description |
|---------|------|-------------|
| `nmap 192.168.1.1` | Default | SYN scan of top 1000 ports |
| `nmap -sn 192.168.1.0/24` | Ping sweep | Find live hosts, no port scan |
| `nmap -sS 192.168.1.1` | SYN scan | Stealthy, no full handshake |
| `nmap -sT 192.168.1.1` | TCP connect | Full handshake, more detectable |
| `nmap -sU 192.168.1.1` | UDP scan | Scan UDP ports |
| `nmap -sV 192.168.1.1` | Version | Identify service versions |
| `nmap -O 192.168.1.1` | OS detect | Guess operating system |
| `nmap -A 192.168.1.1` | Aggressive | OS + version + scripts + traceroute |

---

## Port Specification

```bash
nmap -p 22 192.168.1.1          # Single port
nmap -p 1-1000 192.168.1.1      # Port range
nmap -p- 192.168.1.1            # All 65535 ports
nmap --top-ports 100 192.168.1.1 # Top 100 common ports
```

---

## Reading Output

```
PORT     STATE    SERVICE  VERSION
22/tcp   open     ssh      OpenSSH 8.4
80/tcp   open     http     Apache httpd 2.4
3306/tcp filtered mysql
8080/tcp closed   http-alt
```

| State | Meaning |
|-------|---------|
| open | Service is running and accepting connections |
| closed | Port responded but no service listening |
| filtered | Firewall blocking the probe — no response |

---

## Lab Exercise — Scan Your Own Machine

```bash
ip addr                   # Find your IP
nmap 127.0.0.1            # Scan loopback
nmap -sV 127.0.0.1        # With version detection
nmap -sn 192.168.1.0/24   # Ping sweep your home network (if authorized)
```

Record:
- Which ports are open?
- What services are running?
- Are any unexpected ports open?

---

## Saving Output

```bash
nmap -oN results.txt 192.168.1.1   # Text output
nmap -oX results.xml 192.168.1.1   # XML output
nmap -oA results 192.168.1.1       # All formats
```

---

## Ethics and Safety

- Only scan systems you own or have written permission to scan
- Keep records of authorization for every scan
- In professional work, always have a signed scope of work first
