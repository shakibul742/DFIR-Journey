# Network Fundamentals II

## Coverage

- Days covered: Day 28 to Day 30
- Total days: 3

## Topics Covered

- Introduction to Network Fundamentals 2
- Basic Concepts: unicast, multicast, broadcast, broadcast domain, collision domain, subnet mask
- Virtual Local Area Network (VLAN)
- Virtual Private Network (VPN)
- Network Protocols
- OSI Reference Model
- Media Access Control (MAC) Address
- Address Resolution Protocol (ARP)
- Internet Protocol (IP)
- Internet Control Message Protocol (ICMP)
- Routing

## What I Learned

- Reviewed the core networking concepts needed before protocol analysis.
- Learned the difference between unicast, multicast, and broadcast communication.
- Covered segmentation and isolation concepts such as VLANs, subnets, broadcast domains, and collision domains.
- Reviewed VPN basics, the OSI model, and the role of MAC addressing and ARP in local network communication.
- Built practical understanding around IP addressing, ICMP, and routing behavior.

## Tools Used

- macchanger

## Commands Practiced

```bash
ipconfig
arp -a
ip neigh
sudo ip neigh flush all
sudo resolvectl flush-caches
resolvectl statistics
dig google.com +short
macchanger -l
ping
traceroute
route -n
route print -4
```

## Notes

- This topic built the conceptual base needed for later protocol analysis, packet analysis, and log analysis work.
