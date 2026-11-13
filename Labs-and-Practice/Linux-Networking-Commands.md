# Linux Networking Commands Lab

Run these on Linux (Kali or Ubuntu). Only on systems you own or are authorized to test.

---

## Interface Information

```bash
ip addr
```
Shows all interfaces, IP addresses, and MAC addresses.

```bash
ip link show
```
Shows interface status (UP/DOWN) and MAC addresses.

---

## Routing Table

```bash
ip route
```
Shows the routing table. Look for `default via` to find your gateway.

---

## ARP Table

```bash
arp -a
ip neigh
```
Shows IP-to-MAC mappings cached from recent communication.

---

## DNS

```bash
cat /etc/resolv.conf
```
Shows configured DNS servers.

```bash
dig google.com
nslookup google.com
```
DNS lookups. `dig` shows full response including TTL and record type.

---

## Connectivity Tests

```bash
ping 127.0.0.1          # Test loopback (always works if network stack is running)
ping 192.168.1.1        # Test gateway connectivity
ping 8.8.8.8            # Test internet (no DNS involved)
ping google.com         # Test internet + DNS
traceroute 8.8.8.8      # Trace route to destination
```

---

## Open Ports and Connections

```bash
ss -tuln     # Listening ports only (TCP + UDP, numeric)
ss -tuan     # All connections including established
netstat -tuln # Older alternative
```

Reading `ss -tuln` output:
```
Netid State  Local Address:Port
tcp   LISTEN 0.0.0.0:22          # SSH listening on all interfaces
tcp   LISTEN 127.0.0.1:631       # CUPS listening on loopback only
```

---

## Windows Equivalent Commands

```cmd
ipconfig          # IP, mask, gateway
ipconfig /all     # Full details including MAC and DNS
route print       # Routing table
arp -a            # ARP cache
ping 127.0.0.1
tracert 8.8.8.8
netstat -an
```

---

## Lab Exercise

1. `ip addr` — write down your IP and MAC
2. `ip route` — identify your default gateway
3. `ping 127.0.0.1` — confirm loopback
4. `ping <your gateway>` — confirm gateway is reachable
5. `ping 8.8.8.8` — confirm internet connectivity
6. `ping google.com` — confirm DNS works
7. `traceroute 8.8.8.8` — count hops to reach Google
8. `ss -tuln` — list all listening services
