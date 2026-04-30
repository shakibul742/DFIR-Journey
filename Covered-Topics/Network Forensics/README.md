# Network Forensics

## Coverage

- Foundation days covered: Day 28 to Day 48
- Main track days covered: Day 49, Day 50, Day 52 to Day 54
- Total tracked days: 26
- Status: Completed

## Topics Covered

- Network Fundamentals II
- Network Protocols
- Network Protocols - 2
- Network Packet Analysis
- Network Log Analysis
- Detecting Web Attacks
- Introduction to Network Forensics
- Network Forensics Tools
- Capturing Network Traffic
- Network Traffic Analysis
- Signature-based Detection
- NetFlow-Based Network Forensics
- TLS/SSL Analysis Techniques

## Study Path Overview

| Area | Coverage | Focus Area | Status |
| --- | --- | --- | --- |
| [Network Fundamentals II](<./Network Fundamentals II/README.md>) | Day 28 to Day 30 | Core networking concepts, VLAN, VPN, OSI, ARP, IP, ICMP, and routing | Documented |
| [Network Protocols](<./Network Protocols/README.md>) | Day 31 to Day 34 | TCP, UDP, DNS, and Telnet fundamentals | Documented |
| [Network Protocols - 2](<./Network Protocols - 2/README.md>) | Day 35 | FTP, SSH, HTTP, and DHCP basics | Documented |
| [Network Packet Analysis](<./Network Packet Analysis/README.md>) | Day 36 | Packet capture and analysis tooling workflow | Documented |
| [Network Log Analysis](<./Network Log Analysis/README.md>) | Day 37 to Day 48 | NetFlow, firewall, VPN, proxy, IDS/IPS, WAF, web log, and web attack analysis | Documented |
| Main Network Forensics Track | Day 49, Day 50, Day 52 to Day 54 | Traffic capture, traffic analysis, detection, NetFlow, and TLS/SSL analysis | Completed |

## What I Learned

- Built the networking foundation needed for packet and traffic investigation.
- Reviewed how common protocols behave, including TCP, UDP, DNS, Telnet, FTP, SSH, HTTP, DHCP, TLS, and SSL.
- Practiced capturing network traffic with `tcpdump` and inspecting traffic with Wireshark.
- Learned how to use packet filters to isolate protocols, ports, hosts, and suspicious communication patterns.
- Reviewed network forensics tools such as Wireshark, Tcpdump, Tshark, NetworkMiner, Snort, and Suricata.
- Practiced traffic analysis by identifying useful streams, decoding data, and reviewing service behavior.
- Practiced Detecting Web Attacks with SQL injection, XSS, command injection, IDOR, RFI, and LFI investigation examples.
- Studied signature-based detection and how IDS tools use rules to detect suspicious or malicious traffic.
- Covered NetFlow-based network forensics for reviewing connection metadata and traffic patterns.
- Practiced TLS/SSL traffic analysis concepts and Wireshark filtering for encrypted traffic investigation.

## Tools Used

- Wireshark
- Tcpdump
- Tshark
- NetworkMiner
- Snort
- Suricata
- Netcat
- sqlmap
- Wfuzz
- OWASP Juice Shop
- macchanger
- vsftpd FTP Server
- FileZilla FTP Client

## Commands Practiced

### Network Basics

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

### Protocol and Service Practice

```bash
sudo nc -lvp 5555
dig letsdefend.io
nslookup letsdefend.io
cat /etc/hosts
telnet ip
sudo apt install vsftpd
sudo service vsftpd start
sudo service vsftpd status
sudo service vsftpd stop
sudo apt install openssh-server
sudo service ssh start
sudo service ssh status
sudo service ssh stop
ssh username@SSH_Server_IP_Address
```

### Packet Capture and Traffic Analysis

```bash
sudo tcpdump
sudo tcpdump -D
sudo tcpdump -i wlan0s
tshark -D
tshark -i wlan0
tcpdump -i wlan0 tcp
tcpdump -i wlan0 udp
tcpdump -i wlan0 icmp
tcpdump -i wlan0 arp
tcpdump -i wlan0 port 80
tcpdump -i wlan0 port 443
tcpdump -i wlan0 port 53
tcpdump -i wlan0 tcp port 80
tcpdump -i wlan0 tcp port 443
tcpdump -i wlan0 udp port 53
tcpdump -i wlan0 host 192.168.1.1
tcpdump -i wlan0 src host 192.168.1.1
tcpdump -i wlan0 dst host 192.168.1.1
tcpdump -i wlan0 net 192.168.1.0/24
tcpdump -i wlan0 tcp and port 80
tcpdump -i wlan0 udp and port 53
tcpdump -i wlan0 tcp port 80 or tcp port 443
tcpdump -i wlan0 not icmp
echo "d2VsY29tZQ==" | base64 -d
```

### IDS Practice

```bash
snort -V
snort -r infection-traffic-1.pcap -c /etc/snort/snort.conf
```

### Detecting Web Attacks and Web Log Analysis

```bash
docker run -d -p 3000:3000 bkimminich/juice-shop
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbs --batch
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbms=SQLite --level=5 --risk=3 --technique=E --batch
head http.log
tail http.log
wc -l http.log
less http.log
awk '{print $8}' http.log | sort | uniq -c
awk '$8=="DELETE"' http.log | wc -l
grep -iE "union|select|or 1=1|--|'" http.log
grep -iE "/etc/passwd|/etc/shadow" http.log
grep -iE "admin|login" http.log
grep -i "nmap" http.log
```

### Windows Service Commands

```powershell
Start-Service sshd
Stop-Service sshd
```

## Wireshark Filters Practiced

```text
tcp.flags.syn==1 && tcp.flags.ack==0
tcp.flags.syn==1 && tcp.flags.ack==1
tcp.flags.syn==0 && tcp.flags.ack==1
tcp.flags.syn==1
frame.len==78
dns
dns && ip.addr == 216.239.32.21
dns.a == 216.239.32.21
dns.qry.name == "letsdefend.io"
dns && dns.qry.name == "letsdefend.io"
ftp
http
dhcp
bootp
tcp.port == 9090
tcp.port == 8080
tls
```

## Investigation Highlights

- Used protocol and port filters to reduce packet noise during traffic review.
- Practiced identifying TCP handshake behavior and suspicious SYN-heavy traffic patterns.
- Reviewed DNS queries and hostname resolution artifacts in packet captures.
- Analyzed FTP, HTTP, DHCP, and TLS/SSL traffic from a forensic perspective.
- Reviewed web attack indicators in HTTP logs, including SQL injection, XSS, command injection, IDOR, RFI, and LFI attempts.
- Used Snort with a PCAP file and configuration file to practice signature-based detection.
- Connected packet-level evidence with flow-level thinking through NetFlow-based analysis.

## Key Takeaways

- Network forensics depends on both protocol knowledge and practical packet-analysis skill.
- Packet captures provide deep visibility, while flow and log data help summarize behavior at scale.
- Effective investigation requires filtering, correlation, and an understanding of normal protocol behavior.
- Encrypted traffic still provides useful forensic metadata through TLS/SSL indicators, endpoints, ports, and timing.
