# picoCTF 2026 - Forensics Git 1 Writeup

**Author:** LT "syreal" Jones

**Category:** Forensics

**Difficulty:** Medium (300 pts)

---

## Executive Summary

**Forensics Git 1** extends prior challenges by requiring analysts to recover a flag from **Git commit history** within a disk image. Instead of relying on temporary files, the investigation focuses on **version control artifacts**, specifically commits where sensitive data was added and later removed.

The challenge demonstrates a critical DFIR concept: **data deleted from a Git working directory often persists in repository history**.

---

## Key Concepts

* Raw disk image decomposition (MBR)
* Partition extraction and filesystem carving
* Hidden `.git` repository discovery
* Git commit history analysis
* Data recovery from deleted commits

---

## Tools Used

* **Linux Core Utilities**

  * `find`
* **Archiving / Extraction**

  * `7z`, `7zz`
* **Version Control (Git)**

  * `git log`, `git show`

---

## Methodology

### Step 1: Decompression & Initial Triage

Extract the provided archive:

```bash
7z x disk.img.gz
```

### Observation

* Produces `disk.img` (~1GB)
* Identified as a **raw disk image (MBR)**

---

### Step 2: Partition Extraction

Extract partitions directly:

```bash
7zz x disk.img
```

### Result

* `0.img`
* `1.img` (non-mountable / likely swap)
* `2.img` (valid filesystem)

Extract the valid partition:

```bash
7zz x 2.img -opart2_data
cd part2_data
```

---

### Step 3: Locate Git Repository

Search for hidden `.git` directories:

```bash
find . -type d -name ".git"
```

### Output

```
./home/ctf-player/Code/secrets/.git
```

---

### Step 4: Analyze Git History

Navigate to repository:

```bash
cd home/ctf-player/Code/secrets
```

Inspect commit history:

```bash
git log
```

### Observation

Two key commits:

* **Initial commit** → Added flag
* **Second commit** → Removed flag

---

### Step 5: Recover Deleted Data

View full commit diffs:

```bash
git log -p
```

### Critical Output

```
commit 5fb8194539c770a830b8ba089a50778c07072b03
Author: ctf-player <ctf-player@example.com>
Date:   Wed Nov 19 09:20:05 2025 +0000

    Remove flag

@@ -1 +0,0 @@
-picoCTF{g17_r3m3mb3**_****f904}
```

### Analysis

* File `flag.txt` was deleted
* Git preserves the removed content in history
* The deleted line contains the **flag**

---

### Step 6: Alternative Recovery Method

You can also retrieve the file from the earlier commit:

```bash
git show <commit_hash>
```

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Analyst Notes & Lessons Learned

### 1. The Illusion of Deletion

* Deleting a file in Git does **not erase it**
* Historical data persists unless explicitly rewritten

### 2. Git as a Forensic Goldmine

Sensitive data may exist in:

* Commit history
* Reflogs
* Object database

### 3. Real-World Application

* Common in **credential leaks** (API keys, passwords)
* Frequently exploited in bug bounty and IR

### 4. Efficient Workflow

* `git log -p` is one of the fastest ways to identify sensitive changes
* Always check commit diffs before deeper object analysis

---

## Conclusion

Forensics Git 1 reinforces the importance of examining version control history during investigations. By analyzing commit diffs, we successfully recovered data that appeared deleted, demonstrating how Git can unintentionally preserve sensitive information.

---

## References

* Git Documentation: [https://git-scm.com/docs](https://git-scm.com/docs)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**
