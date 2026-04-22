# picoCTF 2026 - DISKO 4 Writeup

**Author:** Darkraicg492

**Category:** Forensics

**Difficulty:** Medium (200 pts)

---

## Executive Summary

**DISKO 4** is a digital forensics challenge focused on recovering deleted files from a **FAT filesystem**. While the disk image appears normal when mounted, the flag resides in **unallocated space**, requiring forensic tools to uncover.

This challenge reinforces the concept that deleted files often persist on disk and can be recovered using low-level analysis techniques.

---

## Key Concepts

* FAT filesystem analysis
* Deleted file recovery
* Unallocated space inspection
* Inode-based data extraction
* File carving

---

## Tools Used

* **Linux Core Utilities**

  * `file`, `mount`, `cat`
* **Extraction Tools**

  * `7z`
* **The Sleuth Kit (TSK)**

  * `fls`, `icat`

---

## Methodology

### Step 1: Decompression & Triage

Extract the provided archive:

```bash
7z x disko-4.dd.gz
```

Identify filesystem type:

```bash
file disko-4.dd
```

### Observation

* Identified as **FAT (FAT16/FAT32)** filesystem
* Contains standard DOS/MBR boot sector

---

### Step 2: Mounting the Disk (Dead End)

Mount the image:

```bash
mkdir disk
sudo mount -o loop disko-4.dd disk/
ls -la disk/
```

### Observation

* Contains `/log` directory with system logs
* No visible flag or suspicious file

➡️ Indicates target file was **deleted**

---

### Step 3: Identify Deleted Files

List deleted entries using Sleuth Kit:

```bash
fls -rd disko-4.dd
```

### Output

```
r/r * 522629: log/messages
r/r * 532021: log/dont-delete.gz
```

### Analysis

* `*` indicates deleted files
* Suspicious file: `dont-delete.gz`
* Inode: `532021`

---

### Step 4: Recover Deleted Data

Extract raw file data:

```bash
icat disko-4.dd 532021 > recovered-dont-delete.gz
```

---

### Step 5: Extract and Retrieve Flag

Decompress recovered archive:

```bash
7z x recovered-dont-delete.gz
cat dont-delete
```

### Output

```
Here is your flag
```

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Analyst Notes & Lessons Learned

### 1. The Illusion of Deletion

* Deleting a file does not remove its data immediately
* Files remain in unallocated space until overwritten

### 2. FAT Filesystem Behavior

* Directory entry is removed, but data clusters remain
* Recoverable via forensic tools

### 3. Forensics vs Normal Usage

* OS tools (`ls`, file explorer) show only allocated files
* Forensic tools reveal hidden/deleted artifacts

### 4. Importance of Inode-Based Recovery

* `fls` identifies deleted file metadata
* `icat` retrieves raw data directly from disk

---

## Conclusion

DISKO 4 highlights the importance of analyzing unallocated space when investigating disk images. By leveraging Sleuth Kit tools, we successfully recovered a deleted file and extracted the hidden flag, demonstrating how forensic techniques can bypass standard filesystem limitations.

---

## References

* Sleuth Kit: [https://www.sleuthkit.org/](https://www.sleuthkit.org/)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**
