# Module 05 — IPv4 Addressing

## Learning Objectives

- Understand the structure of an IPv4 address
- Convert between decimal and binary
- Understand network ID and host ID
- Identify private and public IP ranges
- Understand CIDR notation and subnet masks

---

## IPv4 Fundamentals

An IPv4 address is a 32-bit number used to identify a device on a network.

Written in **dotted decimal** notation: four decimal numbers (octets) separated by dots.

```
192     .168    .1      .10
11000000.10101000.00000001.00001010
```

Each octet = 8 bits. Four octets × 8 bits = **32 bits total**.

---

## Binary Place Values

```
Bit position:   7    6    5    4    3    2    1    0
Place value:   128   64   32   16    8    4    2    1
```

---

## Decimal to Binary Conversion

Convert 192 to binary:

```
128 → fits once → 1  (remainder 64)
 64 → fits once → 1  (remainder 0)
 32 → no       → 0
 16 → no       → 0
  8 → no       → 0
  4 → no       → 0
  2 → no       → 0
  1 → no       → 0

Result: 11000000
```

| Decimal | Binary |
|---------|--------|
| 192 | 11000000 |
| 168 | 10101000 |
| 128 | 10000000 |
| 10 | 00001010 |
| 255 | 11111111 |
| 0 | 00000000 |

---

## Network ID and Host ID

A subnet mask divides the IP address into two parts:

- **Network ID** — identifies the network
- **Host ID** — identifies the specific device

Example: `192.168.1.10/24`

```
IP:      192.168.1 . 10
Mask:    255.255.255.0
         └─ Network ─┘└Host┘
```

The `/24` means the first 24 bits are the network portion.

---

## Subnet Masks

| CIDR | Subnet Mask | Network Bits | Host Bits |
|------|-------------|-------------|-----------|
| /24 | 255.255.255.0 | 24 | 8 |
| /25 | 255.255.255.128 | 25 | 7 |
| /26 | 255.255.255.192 | 26 | 6 |
| /27 | 255.255.255.224 | 27 | 5 |
| /28 | 255.255.255.240 | 28 | 4 |
| /29 | 255.255.255.248 | 29 | 3 |
| /30 | 255.255.255.252 | 30 | 2 |

---

## Private vs Public IP Ranges

| Range | CIDR | Usage |
|-------|------|-------|
| 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 | Private |
| 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 | Private |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | Private |
| 127.0.0.0 – 127.255.255.255 | 127.0.0.0/8 | Loopback |
| 169.254.0.0 – 169.254.255.255 | 169.254.0.0/16 | APIPA |

**Private IPs** are used inside networks and are not routable on the internet.
**Loopback** (127.0.0.1) refers to your own machine — used for testing.
**APIPA** (169.254.x.x) is auto-assigned when DHCP fails.

---

## Critical Rule

An IP address alone does not tell you the network. You need the subnet mask or CIDR prefix.

`192.168.1.10` could be in `/24`, `/25`, `/26`, or `/27` — the behaviour is completely different.

---

## Cybersecurity Relevance

- Private IPs are targets in internal network attacks and pivoting
- Loopback is used in some exploit payloads
- APIPA exposure suggests a misconfigured or disconnected host

---

## Quick Revision

1. IPv4 = 32 bits = 4 octets
2. Binary place values: 128, 64, 32, 16, 8, 4, 2, 1
3. 255.255.255.0 = /24
4. Private ranges: 10.x, 172.16-31.x, 192.168.x
5. 127.0.0.1 = loopback (your own machine)
6. IP address without mask = incomplete information

---

## Practice Questions

1. Convert 172 to binary
2. What is the subnet mask for /26?
3. Is 10.50.200.1 a private or public address?
4. What does 127.0.0.1 refer to?
5. PC has IP 192.168.1.50/24. What is the network address?
