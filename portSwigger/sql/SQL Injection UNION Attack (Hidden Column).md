# Lab: SQL Injection UNION Attack (Hidden Column)

**Date:** 2024-11-08  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** SQL Injection (Union-Based)

## Key Steps
1. Confirmed SQL injection in the category filter parameter
2. Determined the query returns 2 columns using `ORDER BY` technique
3. Manual `UNION SELECT username, password FROM users--` failed despite correct column names
4. Used sqlmap which revealed a hidden third `email` column with NULL values
5. Successfully extracted credentials using the proper column structure

## Payload
```sql
' UNION SELECT username, password, NULL FROM users--

## Lesson Learned
When a UNION attack with known column names fails despite correct column count, there may be hidden columns not visible in the application's normal output. Database enumeration tools like sqlmap can reveal the complete table structure, and you must match the exact column count in your UNION SELECT, using NULL placeholders for unused columns.