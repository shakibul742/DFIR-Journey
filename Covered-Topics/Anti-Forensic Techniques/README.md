# Anti-Forensic Techniques

## Coverage

- Days covered: Day 05 to Day 08
- Total days: 4

## Topics Covered

- Bootable Media and Portable Application Usage
- Data Hiding Techniques
- Encryption
- Log Tampering and Deletion
- Anonymity Services
- Artifact Wiping
- Case Studies in Anti-Forensics

## What I Learned

- Reviewed common anti-forensic methods attackers use to reduce available evidence.
- Covered data hiding and encryption as ways to obstruct forensic visibility.
- Learned how log tampering, log deletion, and artifact wiping impact investigations.
- Reviewed anonymity services and portable execution methods that reduce traceability.
- Looked at anti-forensic case studies to connect the concepts with real attacker behavior.

## Tools Used

- PowerShell

## Commands Practiced

```powershell
type (Get-PSReadlineOption).HistorySavePath
```

## Notes

- Checked how PowerShell history can be located, which is useful when reviewing artifact wiping or command-history tampering scenarios.
