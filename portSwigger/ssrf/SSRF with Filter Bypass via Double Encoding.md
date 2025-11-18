```markdown
# Lab: SSRF with Filter Bypass via Double Encoding

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Server-Side Request Forgery (SSRF)

## Key Steps
1. Found a vulnerable `stockApi` parameter that was fetched by the backend.
2. Identified two weak filters blocking `localhost` and forward slashes.
3. Bypassed them using a compact loopback IP and double-encoded characters.

## Payload
?stockApi=http://127.1/%2561dmin

## Lesson Learned
Naive filters that block specific characters or strings can often be bypassed with alternative IP representations and multiple layers of encoding.