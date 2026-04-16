# Digital Forensics on Linux

## Coverage

- Days covered: Day 10 to Day 14
- Total days: 5

## Topics Covered

- Introduction to DFIR on Linux
- Linux Live Response 1 and 2
- Linux File Systems
- Linux File System Forensics
- Linux Configuration Files
- Linux System Files

## What I Learned

- Practiced live response with process, user, time, open-file, and network inspection commands.
- Reviewed Linux file systems and basic image acquisition and hash validation workflow.
- Studied high-value Linux artifacts such as `/etc/passwd`, `/etc/shadow`, `/etc/group`, `/etc/sudoers`, `/etc/crontab`, `.bashrc`, `/tmp`, and `/var/tmp`.
- Built a stronger Linux DFIR foundation before moving into Linux memory forensics.

## Tools Used

- top
- htop
- lsof
- netstat
- dc3dd

## Commands Practiced

### Live Response

```bash
ps
ps aux
who
w
last
date
timedatectl
lsof -u debian
lsof -i :9090
netstat -at
netstat -lt
```

### File System Imaging and Validation

```bash
dd if=<source> of=<destination> bs=<block_size> status=progress
mount -o loop,ro /tmp/sda1.img /mnt/image
md5sum filename
sha1sum filename
sha256sum filename
```

### Service, Shell, and Temp-File Investigation

```bash
systemctl status
systemctl list-units --type=service
journalctl -u <service-name>
cat ~/.bashrc
ls -la ~/.bashrc
ls -lart /tmp
ls -lart /var/tmp
find /tmp -name '*.php'
find /var/tmp -name '*.sh'
grep -R "<keyword>" /tmp
find /tmp -mtime -2
find /tmp -size +10M
find /tmp -type f -perm -o=w
```

## Important Artifacts Reviewed

- `/etc/passwd`: user account information
- `/etc/shadow`: password hashes
- `/etc/group`: group memberships
- `/etc/sudoers`: privilege escalation rules
- `/etc/crontab`: scheduled tasks
- `~/.ssh/authorized_keys`: possible unauthorized key persistence
- `~/.bashrc`: possible persistence or malicious command history
- `/tmp` and `/var/tmp`: suspicious scripts, staged files, and writable artifacts

## Notes

- Practiced multiple system monitoring and investigation commands for DFIR use cases.
- Practiced analysis of multiple Linux configuration files and related commands.
