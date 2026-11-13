# Module 08 — Transport Layer

## Learning Objectives

- Explain TCP and UDP
- Describe the TCP three-way handshake
- Understand TCP flags and connection termination
- Explain ports (well-known, registered, ephemeral)
- Use `ss` and `netstat` to inspect connections

---

## TCP vs UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guaranteed delivery | Best effort |
| Order | In-order delivery | No ordering |
| Speed | Slower | Faster |
| Use cases | Web, email, SSH | DNS, VoIP, streaming, gaming |

---

## TCP Three-Way Handshake

```
Client                    Server
  |──── SYN ────────────→ |   "I want to connect. My seq = 100"
  |←─── SYN-ACK ──────── |   "OK. My seq = 200. Ack 101"
  |──── ACK ────────────→ |   "Acknowledged. Let's go."
```

---

## TCP Flags

| Flag | Meaning |
|------|---------|
| SYN | Start connection |
| ACK | Acknowledge |
| FIN | Finish / close connection |
| RST | Reset / abort immediately |
| PSH | Push data to application now |
| URG | Urgent data |

---

## TCP Connection Termination

```
Client                    Server
  |──── FIN ────────────→ |   "I'm done sending"
  |←─── ACK ────────────  |   "Acknowledged"
  |←─── FIN ────────────  |   "I'm done too"
  |──── ACK ────────────→ |   "Closing"
```

---

## Ports

| Range | Type | Description |
|-------|------|-------------|
| 0 – 1023 | Well-known | Standard services |
| 1024 – 49151 | Registered | Registered applications |
| 49152 – 65535 | Ephemeral | Temporary client-side ports |

**Common ports:**

| Port | Protocol | Service |
|------|----------|---------|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 3389 | TCP | RDP |

---

## Practical Commands

```bash
# Show listening ports (Linux)
ss -tuln

# Show all connections
ss -tuan

# Windows
netstat -an
```

---

## Cybersecurity Relevance

- Port scanning discovers open ports — the attack surface
- SYN scan sends SYN but never completes handshake — stealthy
- TCP RST injection can terminate connections
- Listening ports reveal running services

---

## Quick Revision

1. TCP = reliable, ordered, connection-oriented
2. UDP = fast, no guarantee, connectionless
3. 3-way handshake: SYN → SYN-ACK → ACK
4. Well-known ports: 0-1023 (HTTP=80, HTTPS=443, SSH=22)
5. `ss -tuln` shows listening services on Linux

---

## Practice Questions

1. Which protocol for a live video call — TCP or UDP? Why?
2. What three packets make up the TCP handshake?
3. What does the RST flag do?
4. What port range is used for ephemeral ports?
5. Run `ss -tuln` and identify any web or SSH services.
