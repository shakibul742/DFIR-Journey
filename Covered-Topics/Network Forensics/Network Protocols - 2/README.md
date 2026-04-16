# Network Protocols - 2

## Coverage

- Days covered: Day 35
- Total days: 1

## Topics Covered

- File Transfer Protocol (FTP) - 1
- File Transfer Protocol (FTP) - 2
- Secure Shell Protocol (SSH)
- Hypertext Transfer Protocol (HTTP) - 1
- Hypertext Transfer Protocol (HTTP) - 2
- Dynamic Host Configuration Protocol (DHCP)

## What I Learned

- Reviewed how FTP works and why it is risky from a security perspective because it is plaintext.
- Practiced basic FTP server and client setup in the lab.
- Reviewed SSH as the secure alternative for remote access.
- Covered HTTP traffic basics and how web traffic appears in captures.
- Reviewed DHCP traffic and the role of address assignment in network communication.

## Tools Used

- vsftpd FTP Server
- FileZilla FTP Client

## Commands Practiced

### Linux Commands

```bash
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

### Windows Commands

```powershell
Start-Service sshd
Stop-Service sshd
```

## Wireshark Filters Practiced

```text
ftp
http
dhcp
bootp
```
