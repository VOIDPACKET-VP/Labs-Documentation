```markdown
# Lab: SQL Injection UNION Attack (Oracle)

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** SQL Injection (Union-Based)

## Key Steps
1. Determined column count using `ORDER BY`.
2. Enumerated table names via `all_tables` data dictionary.
3. Found column names via `all_tab_columns`.
4. Extracted data from `USERS_ZRLPFO` table.

## Payload
```sql
' UNION SELECT USERNAME_LGRVOX, PASSWORD_LTIQUX FROM USERS_ZRLPFO--

## Lesson Learned
Oracle databases require specific syntax and access to data dictionary views (all_tables, all_tab_columns) for manual enumeration.