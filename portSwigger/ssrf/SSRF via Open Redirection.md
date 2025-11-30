---
vulnerability: SSRF
platform: PortSwigger
difficulty: Medium
date: 2025-11-07
---
**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Server-Side Request Forgery (SSRF)

## Key Steps
1. Found the primary `stockApi` parameter was restricted from accessing other hosts.
2. Discovered an open redirect in the `path` parameter of the `/product/nextProduct` endpoint.
3. Chained the vulnerabilities by feeding the redirect URL into `stockApi`.

## Payload
stockApi=/product/nextProduct?path=http://192.168.0.12:8080/admin

## Lesson Learned
If a vulnerable parameter follows redirects, you can chain it with an open redirect to bypass host restrictions and target internal systems.