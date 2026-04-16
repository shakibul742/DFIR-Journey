# Windows Data Acquisition

## Coverage

- Days covered: Day 02 to Day 04
- Total days: 3

## Topics Covered

- Volatile and Non-Volatile Data on Windows
- Live Data Acquisition on Windows
- Live Data Acquisition Tools
- Dynamic Acquisition on Windows
- Copy and Duplicate on Windows

## What I Learned

- Learned the difference between volatile and non-volatile evidence on Windows systems.
- Practiced the idea of live acquisition on a running host while preserving evidence.
- Reviewed Windows RAM acquisition tooling and initial memory inspection workflow.
- Learned why duplicate imaging and hash verification matter for evidence integrity.
- Compared dynamic acquisition with exact-copy acquisition approaches.

## Tools Used

- WinPmem
- FTK Imager
- Volatility
- Process Explorer
- AutoRuns
- Regedit
- Security Tools
- CertUtil

## Commands Practiced

```powershell
Winpmem_mini_x64_rc2.exe memdump.raw
python .\vol.py -f memdump.mem windows.info.Info
certutil -hashfile memdump.mem SHA256
```

## Notes

- Explored basic concepts of live data acquisition and evidence preservation.
- Learned how WinPmem can capture RAM while keeping forensic handling in mind.
- Verified evidence integrity with SHA256 hashing after acquisition.
