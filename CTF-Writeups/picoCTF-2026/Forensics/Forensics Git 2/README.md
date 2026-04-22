# picoCTF 2026 - Forensics Git 2 Writeup

**Author:** LT "syreal" Jones

**Category:** Forensics

**Difficulty:** Medium (400 pts)

---

## Executive Summary

**Forensics Git 2** represents an advanced DFIR challenge where analysts must recover deleted data from a **corrupted Git repository** embedded within a disk image. Unlike previous tasks, standard Git commands fail due to broken references, requiring manual inspection of Git internals.

The challenge highlights a critical concept: **data in Git persists even when repository structure is damaged**, as long as underlying objects remain intact.

---

## Key Concepts

* Disk image extraction (MBR)
* Hidden Git repository discovery
* Corrupted Git state (broken refs)
* Manual log carving
* Orphaned object recovery

---

## Tools Used

* **Linux Core Utilities**

  * `find`, `cat`
* **Extraction Tools**

  * `7zz`
* **Git Internals**

  * `git show`

---

## Methodology

### Step 1: Decompression & Partition Extraction

Extract the provided archive:

```bash
7zz x disk.img.gz
7zz x disk.img
```

### Result

* `0.img`
* `1.img` (invalid / swap)
* `2.img` (valid filesystem)

Extract filesystem:

```bash
7zz x 2.img -opart2_data
cd part2_data
```

---

### Step 2: Locate Git Repository

Search for `.git` directories:

```bash
find . -type d -name ".git"
```

### Output

```
./home/ctf-player/Code/killer-chat-app/.git
```

---

### Step 3: Identify Corrupted State

Attempt standard Git history analysis:

```bash
git log -p
```

### Error

```
fatal: your current branch 'master' does not have any commits yet
```

### Analysis

* Indicates **broken Git references**
* Likely caused by interrupted deletion
* `.git/refs/heads/master` is missing or corrupted

---

### Step 4: Manual Log Carving

Inspect Git logs manually:

```bash
cat .git/logs/HEAD
```

### Findings

Recovered commit history:

* `2c0a9b...` → Add netcat scripts
* `26b809...` → Add video game chat log
* `582763...` → Add TV show chat log
* `e80b38...` → Add secret hideout chat log
* `2151ef...` → Remove secret hideout log

### Key Insight

The flag is likely inside the **deleted chat log**.

---

### Step 5: Recover Orphaned Commit

Use commit hash from logs to inspect object directly:

```bash
git show e80b38b3322a5ba32ac07076ef5eeb4a59449875
```

### Output (Excerpt)

```
+Rex: Meet at the old arcade basement for the secret hideout.
+Jay: Ask Rusty at the door and use password picoCTF{g17_r35c**_****6bf3}.
+Rex: Bring the decoder map so we can plan the route.
```

### Analysis

* Data recovered from **orphaned Git object**
* Confirms flag embedded in deleted file

---

## 🚩 Final Flag

```text
picoCTF{REDACTED}
```

---

## Analyst Notes & Lessons Learned

### 1. Broken Git ≠ Lost Data

* Git commands rely on references (`refs/`)
* If refs are destroyed, history appears empty
* Underlying objects still exist

### 2. Manual Forensics is Critical

* Inspect `.git/logs/HEAD` for commit traces
* Use hashes to access objects directly

### 3. Git Object Persistence

* Data remains in `.git/objects/`
* Removed only after `git gc`

### 4. Real-World DFIR Relevance

* Attackers may attempt to destroy repository history
* Analysts can still recover data via orphaned objects

---

## Conclusion

Forensics Git 2 demonstrates advanced Git forensics techniques, requiring analysts to bypass broken repository structures and directly interact with Git internals. By manually extracting commit hashes and inspecting orphaned objects, we successfully recovered the hidden flag.

---

## References

* Git Internals: [https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain)
* picoCTF: [https://picoctf.org/](https://picoctf.org/)

---

**Writeup prepared for educational and CTF purposes only.**
