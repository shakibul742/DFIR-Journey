# Challenge: BlackEnergy Lab

| Field | Value |
|------|------|
| Platform | CyberDefenders |
| Category | Memory Forensics |
| Difficulty | Medium |
| Date | 2026-06-29 |


---

## Objectives

- Analyze the provided `.raw` memory capture file and identify hidden suspicious process.

---

## Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Process | `rootkit.exe` |
| PID | `964` |

---

## MITRE ATT&CK

| ID | Technique |
|----|-----------|
| T1014 | Rootkit |

---

## References

- CyberDefenders BlackEnergy Lab
  - https://cyberdefenders.org/blueteam-ctf-challenges/blackenergy/
- MITRE ATT&CK – T1014 Rootkit
  - https://attack.mitre.org/techniques/T1014/