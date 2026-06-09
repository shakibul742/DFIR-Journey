# Email Forensics

## Coverage

- Days covered: Day 55 to Day 56
- Total days: 2
- Status: Completed

## Topics Covered

- Introduction to Email Forensics
- Understanding Email Protocols
- Email Forensics Tools
- Email Header Analysis
- Email Body Analysis
- Email Attachment Analysis
- Identifying and Analyzing Email Threats

## What I Learned

- Reviewed the role of email protocols and mail headers during forensic investigation.
- Practiced tracing email origin using header fields such as `Received` headers.
- Reviewed signs of spoofing, phishing, and suspicious sender infrastructure.
- Practiced email body review and attachment triage for malicious content.
- Connected email artifacts with network and file-analysis workflows.

## Tools Used

- Wireshark
- NetworkMiner
- The Sleuth Kit with Autopsy
- VirusTotal
- Hybrid Analysis
- strings
- Any.Run
- Cuckoo Sandbox
- Joe Sandbox
- VMRay

## Investigation Highlights

- Analyzed sample email headers to identify sender path and suspicious header fields.
- Reviewed email body content for phishing and social engineering indicators.
- Checked attachments for malicious behavior and suspicious embedded content.
- Used sandbox and reputation tools as part of email-threat triage.

## Key Takeaways

- Email forensics requires checking header metadata, message content, attachments, and related network evidence together.
- Spoofed or malicious emails often leave useful indicators across sender infrastructure, headers, URLs, and attachments.
- Attachment analysis should combine static review, reputation checks, and sandbox-style behavior analysis when available.
