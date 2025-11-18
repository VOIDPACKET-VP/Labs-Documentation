```markdown
# Lab: OS Command Injection (Blind, Time-Based)

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** OS Command Injection

## Key Steps
1. Identified a parameter that passed input to a system command.
2. Since output wasn't reflected, used a time-based payload to confirm injection.
3. Injected `sleep 10` to cause a measurable delay in the response.

## Payload
```bash
; sleep 10 ;

## Lesson Learned
Time delays are a reliable technique for confirming blind OS command injection when you cannot see the direct output of your commands.