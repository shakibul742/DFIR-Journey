# picoCTF 2026 - Timeline 1 Writeup

**Author:** LT "syreal" Jones

**Category:** Forensics

**Difficulty:** Medium (300 pts)

---

## Executive Summary

**Timeline 1** builds upon Timeline 0 by introducing large amounts of **system noise** to obscure attacker activity. The challenge requires identifying a hidden flag inside a disk image (`partition4.img`) by leveraging **advanced timeline analysis** and pivoting from attacker anti-forensic behavior.

Unlike the previous challenge, simply filtering for newly created files is insufficient due to the volume of legitimate system activity.

---

## Key Concepts

* Timeline-based forensic analysis
* System noise vs malicious artifacts
* Anti-forensics (log clearing, system shutdown, shredding)
* Unix epoch timestamp correlation
* Inode-based raw extraction

---

## Tools Used

* **Linux Core Utilities**

  * `grep`, `tail`, `base64`
* **The Sleuth Kit (TSK)**

  * `fls`, `mactime`, `icat`

---

## Methodology

### Step 1: Generate the Forensic Timeline

To avoid altering file metadata (especially Access Times), we do **not mount** the disk image. Instead, we directly extract metadata.

```bash
fls -r -m "/" partition4.img > bodyfile.txt
```

Convert it into a readable timeline:

```bash
mactime -b bodyfile.txt > timeline.txt
```

---

### Step 2: Dealing with System Noise

Initial approach: filter for newly created files.

```bash
grep "macb" timeline.txt | tail -n 100
```

### Observation

* Output contains hundreds of legitimate system files
* Mostly related to OS updates (`/etc/ssl/certs/...`)
* Timestamp cluster around **Dec 02 2025 03:42:04**

➡️ Conclusion: This approach is ineffective due to **system noise overwhelming the signal**.

---

### Step 3: Identify the Pivot Point (Anti-Forensics)

Instead of chasing file creation, pivot to attacker behavior.

Search for root history file:

```bash
grep "/root/" bodyfile.txt
```

#### Key Entry

```
/root/.ash_history (inode: 4943)
```

Extract its contents:

```bash
icat partition4.img 4943
```

#### Output

```
poweroff
```

### Analysis

* The attacker issued a **poweroff** command
* Likely intended to:

  * Stop logging
  * Clear volatile memory

This gives us a **critical timestamp anchor**:

```
1764625823
```

---

### Step 4: Epoch Time Correlation

Search for activity occurring around the same time window:

```bash
grep "17646258" bodyfile.txt
```

### Findings

* `/usr/bin/shred` execution → evidence destruction
* `/root/.ash_history` modification
* Suspicious file creation:

```
/etc/chat (inode: 32716)
Timestamp: 1764625807
Size: 49 bytes
```

### Why This Matters

* Created **16 seconds before shutdown**
* Size matches typical encoded flag length
* Located in unusual path (`/etc/`)

➡️ High-confidence malicious artifact

---

### Step 5: Extract and Decode

Extract file using inode:

```bash
icat partition4.img 32716
```

#### Output

```
NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK
```

Decode Base64:

```bash
echo "NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK" | base64 -d
```

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Analyst Notes & Lessons Learned

### 1. System Noise vs Signal

* Large-scale system updates generate massive timeline entries
* Blind filtering (e.g., `macb`) is unreliable

### 2. Importance of Pivoting

* Attacker actions (poweroff, shred) provide **strong investigative anchors**
* Behavioral analysis > blind filtering

### 3. Avoid Live Mounting

* Mounting modifies **Access Time (atime)**
* Can alter forensic evidence (e.g., `macb` → `m.cb`)

### 4. Epoch-Based Hunting

* Direct timestamp searching bypasses filtering issues
* Extremely effective in noisy datasets

---

## Conclusion

Timeline 1 demonstrates how real-world forensic investigations often require analysts to think beyond simple filters. By identifying attacker behavior and pivoting using precise timestamps, we successfully bypassed system noise and recovered the hidden flag.

---

## References

* Sleuth Kit: [https://www.sleuthkit.org/](https://www.sleuthkit.org/)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**