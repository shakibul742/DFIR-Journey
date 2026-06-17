# DFIR with EDR

## Coverage

- Days covered: Day 69 to Day 93
- Total tracked days: 25
- Status: Completed

## Topics Covered

- Introduction to DFIR with EDR
- EDR Utilization in DFIR Plans
- XDR/EDR Threat Analysis & Custom Rule
- Wazuh
- Sysmon Log Analysis

## Subtopic Overview

| Subtopic | Coverage | Focus Area | Status |
| --- | --- | --- | --- |
| [XDR/EDR Threat Analysis & Custom Rule](<./XDR-EDR Threat Analysis and Custom Rule/README.md>) | Day 69 to Day 71, Day 93 | Threat analysis, detection classification, data collection, custom rules, and EDR case scenarios | Completed |
| [Wazuh](<./Wazuh/README.md>) | Day 72 to Day 78, Day 86 to Day 92 | Wazuh architecture, agents, syslog collection, dashboard use, parsing, custom rules, and attack scenarios | Completed |
| [Sysmon Log Analysis](<./Sysmon Log Analysis/README.md>) | Day 79 to Day 85 | Sysmon setup and detections for Mimikatz, Pass-the-Hash, and privilege escalation | Completed |

## What I Learned

- Reviewed how EDR supports incident response through endpoint telemetry, triage, containment, and investigation workflows.
- Studied how EDR and XDR help classify threats and connect host activity with broader detection context.
- Practiced custom detection logic through EDR/XDR rule concepts, Wazuh rules, and Sysmon-supported endpoint telemetry.
- Reviewed Wazuh architecture, agent deployment, log collection, dashboard use, parsing, and correlation.
- Studied Sysmon event collection and detection workflows for credential theft, lateral movement, and privilege escalation behavior.

## Tools Used

- Event Viewer
- EDR/XDR investigation concepts
- Wazuh
- Wazuh Dashboard
- Wazuh Agent
- Sysmon
- SwiftOnSecurity Sysmon Config

## Investigation Highlights

- Reviewed how endpoint telemetry supports detection, triage, containment, and response.
- Practiced log analysis with Event Viewer during EDR-focused scenarios.
- Studied custom detection logic and policy design concepts for endpoint monitoring.
- Reviewed Wazuh dashboard investigation workflows, custom parsing, and custom rule writing.
- Practiced Sysmon-based detection concepts for Mimikatz, Pass-the-Hash, and privilege escalation.
- Reviewed practical cyber incident examples from an endpoint investigation perspective.

## Key Takeaways

- EDR is a core part of modern DFIR because it provides endpoint visibility, response actions, and detection context.
- Custom detection rules should be based on attacker behavior, available telemetry, and tested investigation logic.
- EDR/XDR investigations require correlation between endpoint events, user activity, process behavior, SIEM alerts, and incident timeline.
