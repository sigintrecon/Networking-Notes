# Module 11 — Common Network Protocols

## Learning Objectives

- Know the purpose, default port, and transport for each major protocol
- Understand basic operation
- Identify security considerations

---

## Protocol Reference Table

| Protocol | Port | Transport | Purpose |
|----------|------|-----------|---------|
| HTTP | 80 | TCP | Web traffic (plaintext) |
| HTTPS | 443 | TCP | Web traffic (encrypted) |
| DNS | 53 | TCP/UDP | Name resolution |
| DHCP | 67/68 | UDP | Auto IP assignment |
| SSH | 22 | TCP | Secure remote shell |
| FTP | 21/20 | TCP | File transfer (plaintext) |
| SFTP | 22 | TCP | Secure file transfer (via SSH) |
| SMTP | 25/587 | TCP | Email sending |
| POP3 | 110 | TCP | Email retrieval (downloads, deletes from server) |
| IMAP | 143 | TCP | Email retrieval (keeps on server) |
| SMB | 445 | TCP | File/printer sharing (Windows) |
| RDP | 3389 | TCP | Remote desktop (Windows) |
| NTP | 123 | UDP | Time synchronization |
| SNMP | 161/162 | UDP | Network device management |
| LDAP | 389 | TCP/UDP | Directory services (Active Directory) |
| ICMP | — | IP Protocol 1 | Diagnostics (ping, traceroute) |

---

## Key Protocol Notes

**SSH (22/TCP)** — Replaced Telnet. Use key-based auth. Brute force attacks are common against exposed SSH.

**FTP (20/21/TCP)** — Credentials in plaintext. Never use on untrusted networks. Use SFTP instead.

**SMB (445/TCP)** — Windows file sharing. Major attack target. EternalBlue/WannaCry used SMB.

**RDP (3389/TCP)** — Windows remote desktop. Brute force and credential stuffing attacks are extremely common.

**DNS (53/TCP+UDP)** — UDP for queries, TCP for zone transfers. Zone transfer (AXFR) can expose all DNS records.

**SNMP (161/UDP)** — Default community strings (`public`, `private`) found in many misconfigured devices.

**LDAP (389/TCP)** — Without TLS (LDAPS=636), credentials are plaintext. LDAP enumeration is a core AD attack technique.

---

## TCP vs UDP Summary

**TCP** (reliable): HTTP, HTTPS, SSH, FTP, SMTP, POP3, IMAP, SMB, RDP, LDAP

**UDP** (fast): DNS (queries), DHCP, NTP, SNMP

**Neither** (IP protocol directly): ICMP

---

## Cybersecurity Relevance

- Port scanning reveals which services are exposed
- FTP, Telnet, SNMP v1/v2c, HTTP = plaintext = look for these in packet captures
- RDP, SSH, SMB on exposed ports = high-priority attack surfaces
- Understanding protocols is essential for log analysis, IDS rules, and exploit selection

---

## Quick Revision

1. SSH=22, HTTP=80, HTTPS=443, RDP=3389, SMB=445
2. DNS uses UDP for queries, TCP for zone transfers
3. DHCP and NTP are UDP
4. ICMP is not TCP or UDP — it is IP protocol 1
5. FTP, Telnet, SNMP v1/v2c, HTTP = plaintext = dangerous

---

## Practice Questions

1. What port does SSH use?
2. What is the difference between POP3 and IMAP?
3. Why is FTP considered insecure?
4. What transport does DHCP use?
5. Port 445 is open on a target. What service is likely running and what is the risk?
