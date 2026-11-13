# Module 01 — Networking Fundamentals

## Learning Objectives

By the end of this module you will be able to:

- Explain what a computer network is and why networks exist
- Identify different types of networks (PAN, LAN, WLAN, MAN, WAN)
- Describe client-server and peer-to-peer architectures
- Name common network devices and explain what each one does
- Describe basic network communication

---

## What Is a Computer Network?

A computer network is two or more devices connected together so they can share data and resources.

Everything else — routers, protocols, IP addresses — exists to make that sharing work reliably across different distances and hardware.

---

## Why Do Networks Exist?

Before networks, every computer was an island. If you needed a file from another machine, you physically carried a disk.

Networks solve these problems:

| Problem | Network Solution |
|---------|-----------------|
| Data sharing | Files can be accessed from any connected device |
| Resource sharing | One printer serves many computers |
| Communication | Email, chat, video calls |
| Centralized management | Servers store and manage data for many users |

---

## Types of Networks

| Type | Full Name | Coverage | Example |
|------|-----------|----------|---------|
| PAN | Personal Area Network | ~10 metres | Bluetooth headset to phone |
| LAN | Local Area Network | Building / floor | Office, home, school |
| WLAN | Wireless LAN | Building / campus (wireless) | Wi-Fi network |
| MAN | Metropolitan Area Network | City | University campus network |
| WAN | Wide Area Network | Country / worldwide | The internet |

---

## Network Architectures

### Client-Server

A dedicated machine (the server) provides services. Other machines (clients) request those services.

```
[Client]──┐
[Client]──┼──[Switch]──[Server]
[Client]──┘
```

Examples: web server, email server, file server.

Advantage: Centralized control, easier management.
Disadvantage: If the server fails, all clients lose access.

### Peer-to-Peer (P2P)

Every device can act as both client and server. No central authority.

Advantage: Simple setup, no single point of failure.
Disadvantage: Hard to manage at scale, less secure.

---

## Network Topologies

| Topology | Description | Weakness |
|----------|-------------|----------|
| Bus | All devices on one cable | One break stops everything |
| Star | All devices connect to a central switch | Switch failure stops all |
| Ring | Devices connected in a loop | One failure can stop the ring |
| Mesh | Every device connects to every other | Expensive, complex |

Modern networks almost always use **star topology** with a switch at the centre.

---

## Common Network Devices

| Device | Layer | What It Does |
|--------|-------|--------------|
| Hub | Layer 1 | Repeats electrical signals to all ports — obsolete |
| Switch | Layer 2 | Forwards frames based on MAC addresses |
| Router | Layer 3 | Routes packets between different networks using IP |
| Access Point | Layer 2 | Connects wireless devices to a wired network |
| Modem | Layer 1/2 | Converts signals between your ISP and your home network |

---

## Cybersecurity Relevance

- Understanding network types helps identify attack surfaces
- Client-server architecture is what most web application attacks target
- Rogue access points exploit the trust in wireless networks
- Switches are targeted by MAC flooding attacks

---

## Quick Revision

1. A network = two or more devices connected to share data
2. LAN = local, WAN = wide area (the internet is a WAN)
3. Client requests, server responds
4. Switches use MAC addresses, routers use IP addresses
5. Star topology is standard in modern networks

---

## Practice Questions

1. What is the difference between a switch and a hub?
2. Why can a hub cause performance problems on a busy network?
3. A school has 500 computers across 10 buildings. What type of network is this?
4. Your home Wi-Fi is what type of network?
5. Why does client-server architecture need a reliable server?
