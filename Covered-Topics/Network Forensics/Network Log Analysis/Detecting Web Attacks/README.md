# Detecting Web Attacks

## Coverage

- Days covered: Day 41 to Day 48
- Total days: 8
- Parent topic: [Network Log Analysis](<../README.md>)

## Topics Covered

- Why Detecting Web Attacks Is Important
- OWASP
- How Web Applications Work
- Detecting SQL Injection Attacks
- Database and SQL Basics
- In-Band SQL Injection
- Blind SQL Injection
- Detecting Cross Site Scripting (XSS) Attacks
- Detecting Command Injection Attacks
- Detecting Insecure Direct Object Reference (IDOR) Attacks
- Detecting RFI and LFI Attacks
- Web Log Analysis

## What I Learned

- Reviewed why web attack detection matters for DFIR and SOC investigations.
- Covered OWASP concepts and common web application attack categories.
- Practiced understanding how web applications process requests, parameters, and server responses.
- Studied SQL injection behavior and how suspicious payloads appear in URLs and logs.
- Practiced identifying XSS payloads and reviewing related log evidence.
- Reviewed command injection, IDOR, RFI, and LFI indicators from a detection perspective.
- Used web logs to identify suspicious request methods, source IPs, status codes, user agents, and attack strings.
- Practiced URL decoding as part of web log investigation.

## Tools Used

- sqlmap
- Wfuzz
- OWASP Juice Shop
- Online URL decoder

## Commands Practiced

### SQL Injection Practice

```bash
docker run -d -p 3000:3000 bkimminich/juice-shop
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbs --batch
sqlmap -u "http://localhost:3000/rest/products/search?q=apple" --dbms=SQLite --level=5 --risk=3 --technique=E --batch
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

## Attack Indicators Practiced

- SQL injection keywords and payload patterns such as `union`, `select`, `or 1=1`, comments, and quotes.
- Suspicious successful responses by combining attack-pattern searches with HTTP `200` status results.
- LFI/RFI style file access attempts such as `/etc/passwd` and `/etc/shadow`.
- Admin and login path access patterns.
- Reconnaissance indicators such as `nmap` strings in web logs.
- Unusual request methods such as `DELETE`.
- Suspicious source IP frequency, user agents, and request fields.

## Key Takeaways

- Web attack detection depends heavily on strong log-reading skills.
- URL encoding can hide obvious attack payloads, so decoding is an important investigation step.
- WAF, proxy, IDS/IPS, and web server logs should be correlated during web attack investigations.
- Successful-looking status codes need extra attention when they appear beside suspicious payloads.
