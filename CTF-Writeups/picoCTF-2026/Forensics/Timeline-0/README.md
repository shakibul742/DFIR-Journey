# picoCTF 2026 - Timeline 0 Writeup

**Author:** LT "syreal" Jones

**Category:** Forensics

**Difficulty:** Easy (100 pts)

---

## Executive Summary

**Timeline 0** is a beginner-friendly digital forensics challenge that focuses on identifying and bypassing **timestomping**, an anti-forensics technique used to manipulate file timestamps.

The objective is to locate a hidden flag inside a provided disk image (`partition4.img`). The challenge demonstrates how corrupted or manipulated metadata can break normal filesystem interaction and why forensic tools that operate at a lower level are essential.

---

## Key Concepts

* Timestomping (anti-forensics technique)
* MAC Times (Modified, Accessed, Changed)
* Disk image analysis
* Raw inode-based file extraction
* Base64 decoding

---

## Tools Used

* **Linux Core Utilities**

  * `mount`, `ls`, `head`, `base64`
* **The Sleuth Kit (TSK)**

  * `fls`, `mactime`, `icat`

---

## Methodology

### Step 1: Initial Triage and Mounting

We begin by mounting the disk image to inspect its contents.

```bash
mkdir mount
sudo mount -o loop partition4.img mount/
ls -la mount/
```

### Observation

* Most files have timestamps around **Nov 12**.
* The `/root` directory shows a timestamp of **Dec 2**.

This inconsistency suggests potential tampering, but no flag is visible through standard browsing.

---

### Step 2: Generate a Forensic Timeline

To identify anomalies, we generate a full filesystem timeline.

#### Extract metadata into a bodyfile

```bash
fls -r -m "/" partition4.img > bodyfile.txt
```

#### Convert to human-readable timeline

```bash
mactime -b bodyfile.txt > timeline.txt
```

---

### Step 3: Detect the Timestomped File

Attackers often manipulate timestamps to push files far into the past.

Since the timeline is sorted chronologically (oldest first), inspect the beginning:

```bash
head -n 50 timeline.txt
```

#### Suspicious Entry

```
Tue Jan 01 1985 23:00:00 41 macb r/rrw-r--r-- 0 0 4945 /bin/bcab
```

### Analysis

* The timestamp **1985** is clearly abnormal.
* Indicates **timestomping**.
* File path: `/bin/bcab`
* **Inode Number:** `4945`

---

### Step 4: Raw Data Extraction

Direct access fails due to corrupted metadata:

```bash
cat mount/bin/bcab
```

Error:

```
Bad message
```

To bypass filesystem parsing, extract raw data via inode:

```bash
icat partition4.img 4945
```

#### Output

```
NzFtMzExbj***HU3MTEzcl*****fNDNhMmU3YWYK
```

---

### Step 5: Decode the Payload

The extracted string is Base64 encoded.

```bash
echo "NzFtMzExbj***HU3MTEzcl*****fNDNhMmU3YWYK" | base64 -d
```

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Lessons Learned

* Timestomping can be detected by analyzing chronological anomalies.
* Filesystem mounting is not always reliable when metadata is corrupted.
* Low-level forensic tools like **icat** allow direct inode-based extraction.
* Always inspect both **beginning and end** of timelines.

---

## Conclusion

This challenge reinforces the importance of thinking beyond standard tools when conducting forensic analysis. By leveraging timeline analysis and raw disk extraction, we successfully bypassed metadata manipulation and recovered the hidden flag.

---

## References

* Sleuth Kit Documentation: [https://www.sleuthkit.org/](https://www.sleuthkit.org/)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**
