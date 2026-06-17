# iOS Forensics

## Coverage

- Days covered: Day 59 to Day 60
- Total days: 2
- Status: Completed

## Topics Covered

- iOS Forensics
- iOS File System and APFS
- Handling Locked Backups
- Handling iCloud Data
- Files in Backup Data
- Handling Backup Data

## What I Learned

- Reviewed iOS forensic fundamentals, including iOS security features, APFS, sandboxing, and backup-based evidence access.
- Studied handling locked backups and iCloud data from a forensic perspective.
- Reviewed iOS backup structure and how files can be mapped through backup metadata.
- Practiced SQLite review during iOS artifact analysis.

## Tools Used

- DB Browser for SQLite
- ElcomSoft Phone Breaker
- Magnet AXIOM

## Investigation Highlights

- Analyzed an iOS backup and reviewed extracted phone information.
- Used `Manifest.db` to locate Safari history and bookmark artifacts.
- Identified last-used URL data and bookmark title information from backup records.
- Practiced mapping backup filenames to useful evidence sources.

## Key Takeaways

- iOS forensics often depends on backup structure, encryption state, and available acquisition method.
- Backup databases and metadata are critical for finding application artifacts.
- SQLite review and backup-file mapping are important for building accurate iOS timelines.
