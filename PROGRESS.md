# Learning Progress Tracker

This file tracks my actual learning position. I update it after each study session.

---

## Current Status

**Current lesson:** Routing Tables
**Next up:** Routing between networks, static routes, `route print`, `ip route`

---

## Module Progress

| Module | Topic | Status |
|--------|-------|--------|
| 05 | IPv4 fundamentals | ✅ Completed |
| 05 | IPv4 binary conversion (decimal ↔ binary) | ✅ Completed |
| 05 | Subnet mask concept | ✅ Completed |
| 05 | CIDR notation concept | ✅ Completed |
| 06 | Subnetting calculations (/24 → /30) | 🔄 In Progress |
| 07 | Routing fundamentals (introduction) | ✅ Completed |
| 07 | **Routing Tables** | ⏭ Next Lesson |
| 01 | Networking Fundamentals | 🔲 Not Started |
| 02 | OSI and TCP/IP Models | 🔲 Not Started |
| 03 | Ethernet and MAC | 🔲 Not Started |
| 04 | ARP | 🔲 Not Started |
| 08 | Transport Layer (TCP/UDP) | 🔲 Not Started |
| 09 | Network Services | 🔲 Not Started |
| 10 | Web and Network Security | 🔲 Not Started |
| 11 | Common Network Protocols | 🔲 Not Started |

**Legend:** ✅ Completed | 🔄 In Progress | ⏭ Next Lesson | 🔲 Not Started

---

## What I Have Already Learned

### IPv4 Core Facts

- IPv4 addresses are **32 bits** long
- An IPv4 address has **four octets** (groups of 8 bits)
- Binary place values per octet: **128, 64, 32, 16, 8, 4, 2, 1**
- Decimal 192 in binary = `11000000`

### Subnet Mask to CIDR Mapping (Memorized)

| Subnet Mask | CIDR |
|-------------|------|
| 255.255.255.0 | /24 |
| 255.255.255.128 | /25 |
| 255.255.255.192 | /26 |
| 255.255.255.224 | /27 |

### Key Concepts Understood

- An IP address alone does **not** reveal its actual subnet prefix — the prefix must be supplied through CIDR notation or a subnet mask
- Two PCs on the same Layer 2 switch but in **different IP networks** (e.g. 192.168.1.x/24 and 192.168.2.x/24) need a **router or Layer 3 switch** to communicate

### Routing Scenario Already Studied

```
PC-A: 192.168.1.10/24
PC-B: 192.168.2.20/24
Both connected to the same Layer 2 switch
```

Conclusion: A Layer 2 switch cannot route between these two networks. It operates only at the MAC address level (Layer 2) and has no concept of IP networks or routing decisions.

---

## Study Log

| Date | Topics Covered | Notes |
|------|----------------|-------|
| — | IPv4 addressing, binary conversion | First study session |
| — | Subnet masks, CIDR notation | Manual practice, no calculator |
| — | Subnetting calculations started | /24 to /27 practiced |
| — | Routing fundamentals introduction | Layer 2 vs Layer 3 scenario |

*(Update this after each session)*

---

## Next Session Plan

1. Open Module 07 — Routing
2. Study: What is a routing table?
3. Run `route print` on Windows / `ip route` on Linux
4. Identify columns: destination, subnet mask, gateway, interface
5. Write your own explanation of what each row means
