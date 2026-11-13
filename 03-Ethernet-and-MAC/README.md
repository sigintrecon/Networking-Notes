# Module 03 — Ethernet and MAC

## Learning Objectives

- Explain what Ethernet is and how it works
- Describe the structure of a MAC address
- Distinguish between unicast, multicast, and broadcast
- Understand the Ethernet frame structure
- Explain how a switch learns MAC addresses
- Understand the difference between MAC and IP addresses

---

## Ethernet

Ethernet is the most common wired networking technology. It defines how devices on the same local network communicate using frames.

Ethernet operates at Layer 2 (Data Link) of the OSI model.

---

## MAC Address

Every network interface card (NIC) has a MAC address burned in by the manufacturer.

```
AA:BB:CC:DD:EE:FF
└─ OUI (3 bytes) ─┘└─ Device ID (3 bytes) ─┘
```

- 48 bits total / 6 bytes / 12 hexadecimal characters
- OUI = Organizationally Unique Identifier (assigned to manufacturer)
- Device ID = unique to that specific NIC

---

## Unicast, Multicast, Broadcast

| Type | Destination | Example |
|------|-------------|---------|
| Unicast | One specific device | Normal data transfer |
| Multicast | A group of devices | Video streaming |
| Broadcast | All devices on segment | `FF:FF:FF:FF:FF:FF` |

---

## Ethernet Frame Structure

```
┌──────────┬────────┬───────────┬──────────┬──────────┬──────────┐
│Preamble  │Dst MAC │  Src MAC  │EtherType │   Data   │   FCS    │
│ 8 bytes  │6 bytes │  6 bytes  │ 2 bytes  │ 46-1500B │ 4 bytes  │
└──────────┴────────┴───────────┴──────────┴──────────┴──────────┘
```

- **Preamble**: Synchronization bits so devices know a frame is coming
- **Destination MAC**: Who should receive this frame
- **Source MAC**: Who sent this frame
- **EtherType**: What Layer 3 protocol is inside (0x0800 = IPv4)
- **Data**: The actual payload (IP packet inside)
- **FCS**: Frame Check Sequence — error detection

---

## How a Switch Learns MAC Addresses

A switch has a MAC address table (CAM table). It learns automatically:

1. Frame arrives on port 1 from device with MAC `AA:AA:AA`
2. Switch records: MAC `AA:AA:AA` is on port 1
3. Next frame destined for `AA:AA:AA` → switch sends only to port 1

If the destination MAC is unknown, the switch **floods** the frame to all ports (except incoming) and learns from the reply.

---

## MAC vs IP Address

| | MAC Address | IP Address |
|---|-------------|------------|
| Layer | Layer 2 | Layer 3 |
| Scope | Local network only | Globally routable |
| Format | Hexadecimal (AA:BB:CC) | Decimal (192.168.1.1) |
| Assigned by | Manufacturer | Admin / DHCP |

MAC = delivery within your local network.
IP = delivery across networks and the internet.

---

## Cybersecurity Relevance

- **MAC spoofing**: Attacker changes their MAC to impersonate another device
- **MAC flooding**: Sends fake MAC entries to overflow the CAM table, forcing the switch to broadcast all frames — attacker can then capture all traffic

---

## Practical Commands

```bash
# Show MAC address (Linux)
ip link show

# Show ARP table with MACs
arp -a

# Windows
ipconfig /all
```

---

## Quick Revision

1. MAC address = 48-bit hardware address, used for local delivery
2. Broadcast = `FF:FF:FF:FF:FF:FF`, goes to all devices
3. Switch learns MACs automatically and stores them in CAM table
4. If destination MAC unknown → switch floods
5. MAC is Layer 2, IP is Layer 3

---

## Practice Questions

1. How many bytes is a MAC address?
2. What does a switch do when it receives a frame with an unknown destination MAC?
3. What is the broadcast MAC address?
4. What is the purpose of the FCS field?
5. Can a MAC address be used to route traffic between cities? Why or why not?
