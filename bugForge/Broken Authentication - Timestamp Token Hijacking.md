---
vulnerability: Authentication
platform: BugForge
difficulty: Medium
date: 2025-11-07
---
# CTF: Broken Authentication - Timestamp Token Hijacking

**Date:** 2024-11-07
**Platform:** BugForge.io
**Difficulty:** Medium
**Vulnerability:** Broken Authentication

## Key Steps
1. Discovered the Bearer token was a simple timestamp (`YYYYMMDDHHMMSS`).
2. Found we could hijack any user's session by using their `last_login` timestamp to read their stats via `/api/stats`.
3. Write operations (`/api/session/submit`) validated session ownership, preventing score submission as other users.
4. The intended solution was a numeric brute-force of the token space.

## Lesson Learned
Oversimplified authentication tokens (like raw timestamps) can lead to session hijacking. When you find a vulnerability in read operations but not write, pivot to information disclosure attacks or brute-force the weak token space.