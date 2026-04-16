# Linux Memory Forensics

## Coverage

- Days covered: Day 09, Day 15 to Day 19
- Total days: 6

## Topics Covered

- Introduction to Linux Memory Forensics
- Capturing Memory Dumps
- Analyzing the Memory Dump
- Analysis of the `forensic.lime` file in the LetsDefend Linux lab
- Basic Memory Analysis
- Case Studies and Practical Examples

## What I Learned

- Learned Linux memory forensics basics and how to size and capture memory dumps safely.
- Practiced Linux memory acquisition and reviewed different dump formats and tools.
- Used Volatility to inspect processes, sockets, shell history, loaded modules, and open files from Linux memory images.
- Worked through practical memory-analysis examples using `forensic.lime` and other Linux dumps.
- Built investigation habits by pivoting across processes, commands, files, and network artifacts inside memory.

## Tools Used

- LiME
- Volatility 2
- Volatility 3
- Fmem
- AVML
- Crash
- Memdump
- Coredump

## Commands Practiced

### Memory Capture and Sizing

```bash
df -h
free -m
insmod lime-6.5.0-25-generic.ko "path=/var/dumps/ubuntu-memdump.lime format=lime"
du -sch /var/dumps/ubuntu-memdump.lime
```

### Linux Memory Analysis

```bash
python3 vol.py -f <memory_dump> linux.pslist
python3 vol.py -f <memory_dump> linux.pstree
python3 vol.py -f <memory_dump> linux.psscan
python3 vol.py -f <memory_dump> linux.bash
python3 vol.py -f <memory_dump> linux.lsof
python3 vol.py -f <memory_dump> linux.lsmod
python3 vol.py -f /var/dumps/forensic.lime linux.sockstat
python3 vol.py -f /var/dumps/forensic.lime linux.sockstat | grep 9000
python3 vol.py -f /var/dumps/forensic.lime linux.sockstat | grep 172.16.8.54
python3 vol.py -f /var/dumps/forensic.lime linux.pslist
python3 vol.py -f /var/dumps/forensic.lime linux.lsof
python3 vol.py -f /var/dumps/forensic.lime linux.bash
strings /var/dumps/forensic.lime | grep 172.16.8.54
strings /var/dumps/forensic.lime | grep sshpass
file /var/dumps/forensic.lime
python3 vol.py --help | grep -i linux
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.sockstat --help
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.psaux
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.psscan.PsScan
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.sockstat --pids 829 907
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.bash
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.lsof --pid 838
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.vmayarascan --pid 838
python3 vol.py -f /var/dumps/test-memdump.lime linux.bash | grep wget
python3 vol.py -f /var/dumps/ubuntu-memdump.lime linux.bash | egrep "passwd|shadow"
```

## Notes

- Used Volatility plugins for deeper Linux memory analysis and case-based investigation.
- Explored practical lab examples to correlate process, socket, shell, and file artifacts from memory.
