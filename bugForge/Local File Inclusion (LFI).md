---
vulnerability: LFI
platform: BugForge
difficulty: Easy
date: 2025-11-08
---
# CTF: Local File Inclusion (LFI)

**Date:** 2024-11-08
**Platform:** BugForge.io
**Difficulty:** Easy
**Vulnerability:** File Inclusion

## Key Steps
1. Confirmed LFI by successfully reading `/etc/passwd`.
2. The application indicated the flag was located elsewhere.
3. Pivoted to relative path traversal, which immediately exposed the flag.

## Payload
../flag.txt

## Lesson Learned
When LFI is confirmed but common absolute paths (`/etc/passwd`, `/flag.txt`) don't reveal the flag, immediately switch to relative path traversal (`../`). The flag is often hiding in the application's own directory structure.