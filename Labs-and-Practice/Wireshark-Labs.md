# Wireshark Labs

Wireshark captures and displays network packets in real time.

Only capture on networks you own or have explicit authorization to monitor.

---

## Starting a Capture

1. Open Wireshark
2. Select your interface (usually `eth0` or `wlan0`)
3. Click the blue shark fin to start
4. Click the red square to stop

---

## Essential Display Filters

| Filter | What It Shows |
|--------|--------------|
| `ip.addr == 192.168.1.1` | Traffic to/from that IP |
| `tcp.port == 80` | HTTP traffic |
| `tcp.port == 443` | HTTPS traffic |
| `dns` | All DNS queries and responses |
| `arp` | All ARP packets |
| `icmp` | Ping traffic |
| `tcp.flags.syn == 1` | TCP SYN packets |
| `http.request` | HTTP requests only |

---

## Lab 1 — Capture DNS Traffic

1. Start capture on your active interface
2. Run: `ping google.com`
3. Stop capture
4. Filter: `dns`
5. Find the DNS query and response

Questions:
- What type of record came back?
- What IP was returned for google.com?

---

## Lab 2 — TCP Three-Way Handshake

1. Start capture
2. Run: `curl http://example.com`
3. Stop capture
4. Filter: `tcp.port == 80`
5. Find: SYN → SYN-ACK → ACK

Questions:
- What TCP flags are set on each packet?
- What are the source and destination ports?

---

## Lab 3 — ARP in Action

1. Clear ARP cache: `sudo ip neigh flush all`
2. Start capture
3. Run: `ping 192.168.1.1`
4. Filter: `arp`
5. Find the ARP Request and ARP Reply

Questions:
- What was the destination MAC of the ARP request?
- What MAC address was returned?

---

## Lab 4 — Ethernet Frame Inspection

1. Capture any traffic
2. Click any packet
3. Expand "Ethernet II" in the packet details
4. Record: Source MAC, Destination MAC, EtherType

---

## Useful Features

- **Follow TCP Stream**: Right-click any TCP packet → Follow → TCP Stream
- **Statistics → Protocol Hierarchy**: Breakdown of all protocols
- **Statistics → Endpoints**: All IP addresses and traffic volume

---

## Lab Safety

- Only capture on your own devices and networks
- Do not capture on public Wi-Fi
- Treat captures carefully — they may contain sensitive data
