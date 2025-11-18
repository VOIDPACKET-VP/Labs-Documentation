```markdown
# Lab: SQL Injection - Determining Column Count

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** SQL Injection (Union-Based)

## Key Steps
1. Confirmed SQLi with `' AND 1=2--`.
2. Used incremental `ORDER BY` clauses to find the number of columns.
3. Verified control by injecting a `UNION SELECT` with null values.

## Payload
```sql
' ORDER BY 3--
' UNION SELECT NULL, NULL, NULL--

## Lesson Learned
The ORDER BY technique is a reliable method for determining the number of columns in a vulnerable query, which is the critical first step for a UNION attack.