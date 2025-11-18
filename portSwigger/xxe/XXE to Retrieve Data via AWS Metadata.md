**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** XML External Entity (XXE)

## Key Steps
1. Injected an external entity definition into XML-based stock check.
2. Pointed the entity to the AWS metadata endpoint.
3. Referenced the entity to force the server to fetch the URL.
4. Exfiltrated the IAM security credentials through error messages.

## Payload
```xml
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
&xxe;

## Lesson Learned
Blind XXE can be used to perform SSRF attacks and exfiltrate data from internal services, like cloud metadata endpoints, via out-of-band channels or error messages.