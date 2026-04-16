# Network Protocols

## Coverage

- Days covered: Day 31 to Day 34
- Total days: 4

## Topics Covered

- Introduction to Network Protocols
- Transmission Control Protocol (TCP) - 1
- Transmission Control Protocol (TCP) - 2
- User Datagram Protocol (UDP)
- Domain Name System (DNS) - 1
- Domain Name System (DNS) - 2
- Telnet (Teletype Network) Protocol

## What I Learned

- Reviewed protocol fundamentals and how common network services behave.
- Studied TCP handshakes and connection behavior, including how packet flags appear in traffic.
- Compared TCP with UDP and reviewed where each protocol is commonly used.
- Practiced DNS lookups and basic hostname resolution investigation.
- Reviewed Telnet as a plaintext remote access protocol and compared it conceptually with safer alternatives.

## Tools Used

- netcat
- Wireshark

## Commands Practiced

```bash
sudo nc -lvp 5555
dig letsdefend.io
nslookup letsdefend.io
cat /etc/hosts
telnet ip
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
```

## Notes

- Not all SYN packets indicate normal traffic. Excessive SYN requests can point to malicious behavior.
- Combining multiple packet filters helps detect suspicious patterns more effectively.
- The original daily log included an unclear client-side Netcat command, so only the confirmed command usage is listed here.
