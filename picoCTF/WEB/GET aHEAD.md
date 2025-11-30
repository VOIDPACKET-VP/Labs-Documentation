---
vulnerability: Info Disclosure
platform: picoCTF
difficulty: Easy
date: 2025-11-19
---
# Lab: HTTP Method Vulnerability - HEAD Request Exploitation
- Date: 2025-19-11
- Platform: picoCTF
- Difficulty: Easy
- Vulnerability: Improper HTTP Method Handling & Information Disclosure

## Key Steps
- Code Analysis: Identified different HTTP methods (GET for Red, POST for Blue)
- Method Enumeration: Tested various HTTP methods (PUT, POST, GET, HEAD)
- HEAD Method Discovery: Found that HEAD request returned the flag
- Flag Extraction: Retrieved flag from HEAD response body

## The Vulnerability
- The server improperly handled the HEAD method by:
- Processing it like a GET request
- Returning response body (violating HTTP spec)
- Containing the flag in the response body

## Exploitation
```
HEAD /index.php HTTP/1.1
Host: [target]
```
    - Response contained flag in body despite HEAD spec requiring no body

## Why HEAD Worked
- HTTP Specification Violation: HEAD requests should return headers only, no body
- Improper Method Handling: Server treated HEAD like GET but didn't strip body
- Development Oversight: Common mistake in custom HTTP handlers

## Lesson Learned
- Always validate and properly handle all HTTP methods
- HEAD requests should never return a response body
- Implement method whitelisting for endpoints
- Test all HTTP methods during security assessment
- Development frameworks may handle methods differently

## Remediation
- Implement proper HTTP method handlers
- Reject unsupported methods with 405 Method Not Allowed
- Ensure HEAD returns only headers, identical to GET headers
- Use framework-specific method handling best practices
- Conduct HTTP method security testing


## Real-World Impact:
```Improper HTTP method handling can lead to information disclosure, bypass security controls, and reveal application internals. Many web frameworks have had vulnerabilities related to HEAD method handling.```