# picoCTF 2026 - Forensics Git 0 Writeup

**Author:** LT "syreal" Jones

**Category:** Forensics

**Difficulty:** Medium (200 pts)

---

## Executive Summary

**Forensics Git 0** challenges participants to analyze a raw disk image containing multiple partitions and recover a hidden flag from a Git repository. The task emphasizes partition extraction, targeted triage, and the forensic value of hidden `.git` directories.

The challenge demonstrates how version control artifacts can retain sensitive data even when not visible in the working directory.

---

## Key Concepts

* MBR disk image analysis
* Partition extraction and triage
* String-based artifact discovery
* Git repository forensics
* Hidden metadata recovery

---

## Tools Used

* **Linux Core Utilities**

  * `strings`, `grep`, `cat`
* **Metadata & Extraction Tools**

  * `exiftool`, `7z`

---

## Methodology

### Step 1: Initial Reconnaissance

Determine the file type of the provided image:

```bash
exiftool disk.img
```

### Observation

* Output indicates **unknown or generic binary format**
* Suggests a **raw disk image (MBR)** with multiple partitions

---

### Step 2: Extract Partitions

Use `7z` to quickly extract partitions:

```bash
7z x disk.img
```

### Result

Three partition files are extracted:

* `0.img`
* `1.img`
* `2.img`

---

### Step 3: Targeted String Search

Instead of mounting all partitions, perform a quick triage:

```bash
strings 2.img | grep -i picoCTF
```

### Observation

```
The picoCTF flag format is 'picoCTF{}'
```

➡️ Confirms `2.img` contains relevant data

---

### Step 4: Extract File System

Extract the target partition:

```bash
7z x 2.img -opart2_data
cd part2_data
ls -la
```

### Observation

* Standard Linux filesystem structure
* Includes `/home`, `/root`, `/etc`, etc.

---

### Step 5: Git Repository Analysis

Navigate to user directory:

```bash
cd home/ctf-player/Code/secrets
cat note.txt
```

The file contains only flag format instructions.

#### Check for hidden Git repository

```bash
ls -la
cd .git
ls -la
```

### Key Finding

Presence of `.git` directory containing repository metadata.

---

### Step 6: Recover Commit Message

Inspect Git metadata files:

```bash
cat COMMIT_EDITMSG
```

#### Output

```
Wrap this phrase in the flag format: g17_**_7h3_****_041217d8
```

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Analyst Notes & Lessons Learned

### 1. Efficient Partition Triage

* Tools like `7z` can quickly extract partitions from raw disk images
* Faster than manual offset calculations

### 2. Strings-Based Discovery

* `strings` + `grep` is highly effective for identifying relevant partitions
* Saves time during large-scale investigations

### 3. Git Forensics

* `.git` directories often contain sensitive historical data
* Even deleted files may persist in:

  * `objects/`
  * `logs/`
  * `COMMIT_EDITMSG`

### 4. Hidden Artifacts Matter

* Temporary files (e.g., commit messages) can expose critical information
* Always inspect hidden directories during investigations

---

## Conclusion

Forensics Git 0 highlights the importance of combining efficient triage techniques with deep artifact analysis. By leveraging string searches and Git metadata inspection, we successfully recovered the hidden flag without needing full filesystem mounting.

---

## References

* Git Documentation: [https://git-scm.com/docs](https://git-scm.com/docs)
* Sleuth Kit: [https://www.sleuthkit.org/](https://www.sleuthkit.org/)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**
