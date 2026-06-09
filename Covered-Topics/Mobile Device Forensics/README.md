# Mobile Device Forensics

## Coverage

- Days covered: Day 57 to Day 60
- Total days: 4
- Status: Completed

## Topics Covered

- Android Forensics
- Android File System
- Handling Locked Android Devices
- Evidentiary Data on Android
- Android Forensics Tools
- iOS Forensics
- iOS File System and APFS
- Handling Locked Backups
- Handling iCloud Data
- iOS Backup Files and Backup Data Handling

## What I Learned

- Reviewed Android and iOS forensic fundamentals, including file-system structure and evidence sources.
- Practiced working with Android evidence extracted through forensic tooling.
- Reviewed common mobile artifacts stored in SQLite databases.
- Practiced timestamp conversion during mobile artifact review.
- Reviewed iOS backup structure and how files can be mapped through backup metadata.

## Tools Used

- Andriller
- AndroidQF
- adb
- DB Browser for SQLite
- ElcomSoft Phone Breaker
- Magnet AXIOM

## Commands Practiced

```bash
adb devices
adb shell
date -u -d @1713348618
```

## Investigation Highlights

- Analyzed an Andriller output file and reviewed extracted Android artifacts.
- Identified first camera access time and converted a Unix timestamp into readable UTC time.
- Used DB Browser for SQLite to inspect mobile application data.
- Analyzed an iOS backup and used `Manifest.db` to locate Safari history and bookmark artifacts.
- Identified phone information, last-used URL data, and bookmark title information from backup records.

## Key Takeaways

- Mobile forensics depends heavily on understanding platform storage, backup structure, and application databases.
- SQLite review is a core skill for both Android and iOS artifact analysis.
- Timestamp handling and backup-file mapping are important for building accurate mobile timelines.
