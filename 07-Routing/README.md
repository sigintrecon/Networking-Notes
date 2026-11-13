# Module 07 — Routing

> This is your **next lesson** — Routing Tables.

## Learning Objectives

- Explain what routing is and why it is needed
- Understand the default gateway
- Read and interpret a routing table
- Distinguish between connected, static, and default routes
- Understand Longest Prefix Match (LPM)
- Use `ip route` and `route print` to inspect routing tables
- Trace a packet through multiple routers

---

## What Is Routing?

Routing is the process of deciding which path a packet should take to reach its destination.

A switch handles delivery **within** a network (Layer 2, using MAC addresses).
A router handles delivery **between** networks (Layer 3, using IP addresses).

If your packet needs to leave your local network — to reach a server in another city or even another subnet in the same building — it goes through a router.

---

## Why Routing Is Needed

```
Network A: 192.168.1.0/24          Network B: 192.168.2.0/24
PC-A: 192.168.1.10                 PC-B: 192.168.2.20
              |                              |
           [Switch]                       [Switch]
              |                              |
        [Router Port 1]────────────[Router Port 2]
        192.168.1.1                   192.168.2.1
```

PC-A cannot reach PC-B through the switch alone. The switch only understands MAC addresses on its own LAN segment.

PC-A sends the packet to its **default gateway** (192.168.1.1). The router checks its routing table and forwards the packet toward 192.168.2.0/24.

---

## Default Gateway

The default gateway is the router's IP address on your local network. It is where your device sends packets when the destination is NOT on your local subnet.

```
Your PC:         192.168.1.10/24
Default gateway: 192.168.1.1
```

When you send a packet to 8.8.8.8:
1. Your PC checks: is 8.8.8.8 on my /24 network? No.
2. PC sends the packet to gateway 192.168.1.1
3. The router handles it from there

---

## The Routing Table

A routing table is the list of known networks and how to reach them.

Every router and every PC has one.

### Linux — `ip route` output

```
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.10
10.0.0.0/8 via 192.168.1.1 dev eth0
```

| Destination | Via (Next Hop) | Interface | Meaning |
|-------------|---------------|-----------|---------|
| default | 192.168.1.1 | eth0 | Send everything unknown to gateway |
| 192.168.1.0/24 | directly connected | eth0 | This is my own network |
| 10.0.0.0/8 | 192.168.1.1 | eth0 | Reach 10.x.x.x via gateway |

### Windows — `route print` output

```
Network Destination   Netmask         Gateway       Interface   Metric
0.0.0.0               0.0.0.0         192.168.1.1   192.168.1.10   25
192.168.1.0           255.255.255.0   On-link       192.168.1.10   281
127.0.0.0             255.0.0.0       On-link       127.0.0.1      331
```

**Columns explained:**

| Column | Meaning |
|--------|---------|
| Network Destination | Destination network |
| Netmask | Subnet mask for that destination |
| Gateway | Where to send the packet next |
| Interface | Which local interface to use |
| Metric | Cost — lower metric = preferred route |

---

## Types of Routes

### Connected Route

A network directly attached to one of the router's interfaces. Added automatically when an interface comes up.

```
Router has 192.168.1.1/24 → Connected route for 192.168.1.0/24 (automatic)
```

### Static Route

A manually configured route.

```bash
# Linux
ip route add 10.0.0.0/8 via 192.168.1.1

# Windows
route add 10.0.0.0 mask 255.0.0.0 192.168.1.1
```

### Default Route

Catches all traffic that does not match any more specific route.

```
Destination: 0.0.0.0/0
Gateway:     192.168.1.1
```

This is the "if you don't know where it goes, send it here" rule.

---

## Longest Prefix Match (LPM)

When a router has multiple routes matching the same destination, it uses the **most specific** (highest CIDR number) route.

**Example routing table:**
```
10.0.0.0/8      via 192.168.1.1
10.1.0.0/16     via 192.168.1.2
10.1.1.0/24     via 192.168.1.3
0.0.0.0/0       via 192.168.1.1
```

Destination packet: **10.1.1.50**

| Route | Match? |
|-------|--------|
| 10.0.0.0/8 | Yes (8-bit match) |
| 10.1.0.0/16 | Yes (16-bit match) |
| 10.1.1.0/24 | Yes (24-bit match) ← **Winner** |

Packet goes via 192.168.1.3.

---

## Packet Forwarding Decision (Step by Step)

When a router receives a packet:

1. Look at destination IP address
2. Compare destination against every routing table entry
3. Find all matching entries
4. Select the entry with the **longest prefix** (most specific)
5. Forward packet to the specified next hop
6. If no match at all → packet is dropped

---

## Practical Commands

### Linux

```bash
# Show routing table
ip route
ip route show

# Add static route
ip route add 10.0.0.0/8 via 192.168.1.1

# Add default gateway
ip route add default via 192.168.1.1

# Delete a route
ip route del 10.0.0.0/8
```

### Windows

```cmd
# Show routing table
route print

# Add static route
route add 10.0.0.0 mask 255.0.0.0 192.168.1.1

# Add persistent route (survives reboot)
route -p add 10.0.0.0 mask 255.0.0.0 192.168.1.1
```

---

## Real-World Scenario

**Your laptop sends a request to 142.250.80.46 (Google):**

```
1. PC checks: is 142.250.80.46 on 192.168.1.0/24? No.
2. Check routing table → matches default route 0.0.0.0/0 via 192.168.1.1
3. ARP for gateway MAC (192.168.1.1)
4. Send frame to gateway MAC containing IP packet to 142.250.80.46
5. Router receives it, checks its own routing table
6. Router forwards packet toward Google through upstream connection
7. Multiple hops across the internet until Google is reached
```

---

## Cybersecurity Relevance

- `route print` and `ip route` are early post-exploitation commands to understand the target network layout
- Default route manipulation can redirect all traffic through an attacker
- Understanding routing tables is essential for network recon and pivot planning
- /32 host routes are used in advanced attack routing scenarios

---

## Common Mistakes

1. Forgetting the default gateway — most common reason a PC "can't reach the internet"
2. Confusing the PC's routing table with the router's routing table — both have one
3. Not understanding that LPM always wins — a /24 beats a /8 for the same destination
4. Adding a static route without a return route — traffic needs a path both ways

---

## Quick Revision

1. Router = forwards packets between networks using IP
2. Default gateway = router's IP on your LAN
3. Routing table = list of destinations and next hops
4. Connected route = directly attached (automatic)
5. Static route = manually added
6. Default route = 0.0.0.0/0 catches everything not matched
7. LPM = most specific route wins

---

## Practice Questions

1. PC has 10.0.0.5/8, gateway 10.0.0.1. It wants to reach 172.16.1.1. What happens step by step?
2. Routing table has 192.168.0.0/16 and 192.168.1.0/24. Packet arrives for 192.168.1.50. Which route wins?
3. What does `0.0.0.0/0` mean in a routing table?
4. Run `route print`. Identify the default route entry.
5. What is the difference between a connected route and a static route?
6. Why do you need a return route when adding a static route?
