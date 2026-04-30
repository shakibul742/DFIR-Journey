# Network Log Analysis

## Coverage

- Days covered: Day 37 to Day 48
- Total days: 12

## Topics Covered

- Generic Log Analysis (Netflow)
- Firewall Log Analysis
- VPN Log Analysis
- Proxy Log Analysis
- IDS/IPS Log Analysis
- WAF Log Analysis
- Web Log Analysis
- [Detecting Web Attacks](<./Detecting Web Attacks/README.md>)

## What I Learned

- Reviewed generic network log analysis as a prerequisite for future network forensics work.
- Practiced extracting useful fields and counts from firewall logs with command-line filtering.
- Covered how firewall and VPN logs can provide visibility into connection behavior and access patterns.
- Reviewed proxy, IDS/IPS, and WAF logs as important sources for network and web attack investigation.
- Practiced web log analysis for identifying request methods, source IPs, status codes, user agents, and suspicious URL patterns.
- Studied how web attacks appear in logs, including SQL injection, XSS, command injection, IDOR, RFI, and LFI attempts.

## Tools Used

- sqlmap
- Wfuzz
- OWASP Juice Shop
- Online URL decoder

## Commands Practiced

### Firewall Log Analysis

```bash
grep -o "action=[a-z]*" firewall.txt | grep -o "dstport=[0-9]*" firewall.txt | cut -d= -f2 | sort | uniq -c
grep -o grep -o "dstport=[0-9]*" firewall.txt | cut -d= -f2 | sort -u | wc -l
```

### Web Log Analysis

```bash
head http.log
tail http.log
wc -l http.log
less http.log
awk '{print $8}' http.log | sort | uniq -c
awk '$8=="DELETE"' http.log | wc -l
awk '{print $3}' http.log | sort | uniq -c | sort -nr
awk '{print $3}' http.log | sort | uniq -c | sort -nr | head -1
grep -iE "union|select|or 1=1|--|'" http.log
grep -iE "union|select|or 1=1|--|'" http.log | grep " 200 "
grep -iE "union|select|or 1=1|--|'" http.log | grep " 200 " | wc -l
grep -i "union" http.log | awk '{print $3}' | sort | uniq -c | sort -nr
awk '{print $10}' http.log | sort | uniq -c | sort -nr | head
grep -iE "/etc/passwd|/etc/shadow" http.log
grep -iE "admin|login" http.log
grep -i "nmap" http.log
grep " 200 " http.log
awk '{print $13}' http.log
awk '{print $17}' http.log
```

### Detecting Web Attacks Practice

```bash
docker run -d -p 3000:3000 bkimminich/juice-shop
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbs --batch
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbms=SQLite --level=5 --risk=3 --technique=E --batch
```

## Subtopics

| Subtopic | Coverage | Focus Area | Status |
| --- | --- | --- | --- |
| [Detecting Web Attacks](<./Detecting Web Attacks/README.md>) | Day 41 to Day 48 | OWASP basics, SQL injection, XSS, command injection, IDOR, RFI, LFI, and web log investigation | Documented |

## Notes

- This topic is organized here as part of the prerequisite path before starting the main `Network Forensics` topic.
- Web attack detection is included under Network Log Analysis because most investigation practice focused on reading web, WAF, proxy, and IDS/IPS logs.
