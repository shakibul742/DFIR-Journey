# Windows Memory Forensics

## Coverage

- Days covered: Day 20 to Day 27
- Total days: 8

## Topics Covered

- Introduction to Windows Memory Forensics
- Capturing Memory Dumps
- Analyzing the Memory Dump
- Basic Memory Analysis
- Case Studies and Practical Examples: port scan detection, brute force detection, and credential dumping detection

## What I Learned

- Learned the overall Windows memory forensics workflow from capture to analysis.
- Reviewed multiple memory capture tools for Windows environments.
- Used Volatility and Rekall style workflows to inspect processes, modules, drivers, registry artifacts, command lines, and network connections.
- Practiced basic memory hunting with process review, hidden process discovery, and YARA-based searching.
- Used memory artifacts to recognize attacker behavior such as scanning, brute force attempts, and credential dumping.
- Built the habit of correlating process, command-line, and network evidence during investigation.

## Tools Used

- AccessData FTK Imager
- Volatility 3
- WinDbg
- Magnet RAM Capture
- Belkasoft Evidence Center
- Rekall
- MemDump

## Commands Practiced

### Core Windows Memory Analysis

```powershell
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.info
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.hashdump
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.pslist
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.dlllist
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.malfind
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.pstree
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.driverscan
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.drivermodule
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.psscan
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.cmdline
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.registry.hivelist
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.registry.hivescan
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.modules
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem windows.netscan
python vol.py -f C:\Users\LetsDefend\Desktop\fr01.mem yarascan.YaraScan --yara-file rule.yar
```

### Generic Practice Commands Logged During Case Study Work

```powershell
python vol.py -f <memory_dump> windows.pslist
python vol.py -f <memory_dump> windows.cmdline
python vol.py -f <memory_dump> windows.netscan
```

## Investigation Highlights

- Enumerated running and hidden processes with `pslist` and `psscan`.
- Analyzed command-line activity with `cmdline` to find suspicious execution history.
- Investigated live connections with `netscan`.
- Applied a YARA rule to detect the `net user` command inside memory.
- Used manual string searching to validate findings and locate related artifacts.

## Case Study Insights

- Port Scan Detection:
  Identified `nmap.exe`, reviewed command-line evidence, and recognized internal reconnaissance behavior.
- Brute Force Detection:
  Observed repeated `SYN_SENT` style connection attempts and tied network activity back to processes.
- Credential Dumping Detection:
  Identified `mimikatz.exe`, reviewed dumping commands, and understood LSASS targeting behavior.

## Key Takeaways

- Memory forensics exposes live attacker activity that may never be fully visible on disk.
- Correlating process, command-line, and network artifacts improves detection accuracy.
- Understanding attack flow helps explain what an attacker was trying to do on the host.
