# Pexel Whisperer

## Challenge Information

* Event: Robofest EWU CTF 2026

## Objective

Analyze the provided PNG image and identify any hidden data.

## Investigation Steps

1. Checked file type and metadata using `file` and `exiftool`.
2. Verified PNG structure using `pngcheck`.
3. Enumerated embedded signatures using `binwalk`.
4. Performed LSB analysis using `zsteg`.

## Key Finding

Hidden text discovered in the Red channel Least Significant Bit (LSB):

ROBOFEST{lsb_1s_******_w4t**ing}

## Tools Used

* file
* exiftool
* pngcheck
* binwalk
* zsteg

## Lessons Learned

A PNG can appear completely normal while containing hidden data in pixel LSBs. Traditional file-carving tools may not detect this technique.
