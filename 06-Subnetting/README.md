# Module 06 — Subnetting

## Learning Objectives

- Calculate network address, broadcast address, and usable host range
- Determine the number of usable hosts per subnet
- Work with CIDR prefixes /24 through /30
- Understand VLSM fundamentals
- Solve practical subnetting problems

---

## Why Subnet?

Subnetting divides a large IP network into smaller sub-networks.

Benefits: better security, reduced broadcast traffic, efficient IP address use, easier troubleshooting.

---

## Key Formula

```
Usable hosts = 2^(host bits) - 2

(Subtract 2: one for network address, one for broadcast address)
```

---

## Subnetting Reference Table

| CIDR | Subnet Mask | Host Bits | Total | Usable Hosts |
|------|-------------|-----------|-------|--------------|
| /24 | 255.255.255.0 | 8 | 256 | 254 |
| /25 | 255.255.255.128 | 7 | 128 | 126 |
| /26 | 255.255.255.192 | 6 | 64 | 62 |
| /27 | 255.255.255.224 | 5 | 32 | 30 |
| /28 | 255.255.255.240 | 4 | 16 | 14 |
| /29 | 255.255.255.248 | 3 | 8 | 6 |
| /30 | 255.255.255.252 | 2 | 4 | 2 |

---

## Worked Example — /26

**Given:** 192.168.1.0/26 — Block size = 64

| Subnet | Network | Usable Range | Broadcast |
|--------|---------|-------------|-----------|
| 1 | 192.168.1.0 | .1 – .62 | .63 |
| 2 | 192.168.1.64 | .65 – .126 | .127 |
| 3 | 192.168.1.128 | .129 – .190 | .191 |
| 4 | 192.168.1.192 | .193 – .254 | .255 |

**Rules:**
- Network address = first address (all host bits = 0)
- Broadcast address = last address (all host bits = 1)
- Usable hosts = everything between

---

## Worked Example — /30

**Given:** 10.0.0.0/30 — Block size = 4

| Field | Value |
|-------|-------|
| Network | 10.0.0.0 |
| First usable | 10.0.0.1 |
| Last usable | 10.0.0.2 |
| Broadcast | 10.0.0.3 |
| Usable hosts | 2 |

/30 is used for point-to-point links between two routers.

---

## Practice Exercises

**Exercise 1:** What is the broadcast address of 192.168.5.0/27?

<details>
<summary>Answer</summary>
Block size = 32. Network = 192.168.5.0, Broadcast = 192.168.5.31
</details>

**Exercise 2:** How many usable hosts does /29 provide?

<details>
<summary>Answer</summary>
2^3 - 2 = 6 usable hosts
</details>

**Exercise 3:** PC has IP 10.10.10.200/28. What network is it in?

<details>
<summary>Answer</summary>
Block size = 16. Subnets: .0, .16, .32...192, .208. 200 falls in .192 block.
Network = 10.10.10.192/28
</details>

---

## VLSM — Variable Length Subnet Masking

VLSM allows different subnets within the same network to have different prefix lengths — avoiding waste.

Example:
- Headquarters (100 hosts) → /25 (126 usable)
- Branch (20 hosts) → /27 (30 usable)
- Point-to-point link (2 hosts) → /30 (2 usable)

---

## Cybersecurity Relevance

- Understanding subnets helps map a target network's structure during recon
- /30 on a router link is a common discovery
- Subnets define broadcast domains — scope of ARP and some attacks

---

## Quick Revision

1. Host bits = 32 - prefix length
2. Usable hosts = 2^(host bits) - 2
3. /30 = 2 usable hosts (point-to-point)
4. Network address = all host bits zero
5. Broadcast address = all host bits one

---

## Practice Questions

1. How many usable hosts does /25 provide?
2. What is the network address of 172.16.5.70/26?
3. What prefix do you use for a link between exactly two routers?
4. What is the broadcast address of 192.168.100.128/25?
5. A company needs subnets of 12 hosts each. What prefix should they use?
