# Android Forensics

## Coverage

- Days covered: Day 57 to Day 58
- Total days: 2
- Status: Completed

## Topics Covered

- Android Forensics
- Android File System
- Handling Locked Android Devices
- Evidentiary Data on Android
- Android Forensics Tools

## What I Learned

- Reviewed Android forensic fundamentals, including platform storage, file-system structure, and evidence sources.
- Studied common approaches for handling locked Android devices during forensic review.
- Practiced working with Android evidence extracted through forensic tooling.
- Reviewed common mobile artifacts stored in SQLite databases.
- Practiced timestamp conversion during mobile artifact review.

## Tools Used

- Andriller
- AndroidQF
- adb
- DB Browser for SQLite

## Commands Practiced

```bash
adb devices
adb shell
date -u -d @1713348618
```

## Investigation Highlights

- Analyzed an Andriller output file and reviewed extracted Android artifacts.
- Identified first camera access time and converted a Unix timestamp into readable UTC time.
- Used DB Browser for SQLite to inspect Android application data.
- Practiced using `adb` for basic Android device interaction.

## Key Takeaways

- Android forensics depends heavily on understanding platform storage, application data, and acquisition limits.
- SQLite review is a core skill for Android artifact analysis.
- Timestamp handling is important for building accurate mobile timelines.
