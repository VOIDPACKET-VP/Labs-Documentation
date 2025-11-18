```markdown
# Lab: JWT Authentication Bypass via JKU Injection

**Date:** 2024-11-07  
**Platform:** PortSwigger Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Broken Authentication

## Key Steps
1. Generated a malicious RSA key pair in Burp Suite.
2. Hosted the public key as a JWK Set on the exploit server.
3. Forged a JWT with a `jku` header pointing to my JWK Set.
4. Signed the token with my private key and submitted it.

## Payload
JWT Header:
```json
{
  "alg": "RS256",
  "typ": "JWT",
  "jku": "https://exploit-server.net/exploit",
  "kid": "malicious-key-id"
}

## Lesson Learned
Servers that trust arbitrary jku (JWK Set URL) parameters without a domain allowlist are vulnerable to signature bypass attacks.