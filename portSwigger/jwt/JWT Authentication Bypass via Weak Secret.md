---
vulnerability: JWT Manipulation
platform: PortSwigger
difficulty: Medium
date: 2025-11-07
---
# Lab: JWT Authentication Bypass via Weak Secret

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Broken Authentication

## Key Steps
1. Captured a JWT from the application.
2. Used Hashcat (mode 16500) to brute-force the signing key.
3. The key `secret1` was found in the wordlist.
4. Used `jwt_tool` to forge a new token with an "administrator" role.

## Payload
Brute-force command:
```bash
hashcat -m 16500 <jwt> /usr/share/wordlists/jwt.secrets.list

## Lesson Learned
Using weak, predictable secrets for signing JWTs allows an attacker to forge arbitrary tokens and bypass authentication entirely.