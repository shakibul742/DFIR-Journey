# Sysmon Log Analysis

## Coverage

- Days covered: Day 79 to Day 85
- Total days: 7
- Status: Completed

## Topics Covered

- Introduction and Setup of Sysmon
- SwiftOnSecurity Sysmon Configuration
- Detecting Mimikatz with Sysmon
- Detecting Pass-the-Hash with Sysmon
- Detecting Privilege Escalation with Sysmon

## What I Learned

- Reviewed Sysmon as a Windows telemetry source for process, network, and system activity.
- Practiced installing Sysmon with a known community configuration.
- Studied detection workflows for credential theft, lateral movement, and privilege escalation behavior.
- Reviewed how Sysmon events can support endpoint investigation and timeline building.

## Tools Used

- Sysmon
- SwiftOnSecurity Sysmon Config
- Event Viewer

## Commands Practiced

```powershell
Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

## Investigation Highlights

- Installed Sysmon using the SwiftOnSecurity configuration.
- Reviewed Mimikatz detection concepts through Sysmon telemetry.
- Reviewed Pass-the-Hash detection concepts through Windows event and Sysmon activity.
- Reviewed privilege-escalation detection scenarios with Sysmon data.

## Key Takeaways

- Sysmon provides high-value Windows telemetry for DFIR and detection engineering.
- A strong Sysmon configuration improves visibility into suspicious endpoint behavior.
- Sysmon events become more useful when correlated with EDR, SIEM, and Windows Event Log data.
