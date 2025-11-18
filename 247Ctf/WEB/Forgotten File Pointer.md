# Lab: PHP LFI via File Descriptor Inclusion
- Date: 2025-17-11
- Platform: 247CTF
- Difficulty: Moderate
- Vulnerability: Local File Inclusion & File Descriptor Abuse

## Key Steps
- Code Analysis: Identified the PHP script opens /tmp/flag.txt and allows file inclusion with ≤10 character limit
- Linux File System Understanding: Recognized that in Linux "everything is a file" including file descriptors
- File Descriptor Discovery: Used the /dev/fd/ directory to access open file descriptors
- Brute Force Approach: Systematically tested file descriptors 0-99 to find which one contained the flag
- Flag Extraction: Found that file descriptor 10 contained the flag content

## Payload
- Brute force file descriptors 0-99
```
for i in $(seq 0 99); do 
    echo "Testing fd $i"
    curl -s "https://target.247ctf.com/?include=/dev/fd/$i" | grep 247CTF
done
```
## Working payload:
- ?include=/dev/fd/10

## Why It Works
- PHP's fopen() opens /tmp/flag.txt before the include check
- The file remains open as a file descriptor during script execution
- Linux exposes open file descriptors via /dev/fd/ directory
- File descriptor 10 happened to be the one holding the open flag file
- /dev/fd/10 is exactly 10 characters, fitting the length constraint

## Lesson Learned
- Linux file descriptors can be accessed via /dev/fd/ pseudo-filesystem
- Open files in PHP remain accessible via their file descriptors
- When dealing with character limits, creative path shortening is essential
- "Everything is a file" in Linux extends to process file descriptors
- Brute forcing small ranges (like 0-99) is feasible and effective in CTFs