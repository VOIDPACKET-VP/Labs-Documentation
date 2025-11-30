---
vulnerability: SQLi
platform: PortSwigger
difficulty: Medium
date: 2025-11-07
---
# Lab: SQL Injection - Finding String-Compatible Columns

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** SQL Injection (Union-Based)

## Key Steps
1. Already knew the query had 3 columns from previous recon.
2. Systematically replaced `NULL` placeholders in a `UNION SELECT` with a test string.
3. Identified the second column as compatible with string data.

## Payload
```sql
' UNION SELECT NULL, 'nxb255', NULL--

## Lesson Learned
After finding the number of columns, you must identify which ones can return string data to exfiltrate text-based information.