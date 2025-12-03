---
vulnerability: BAC
platform: picoCTF
difficulty: Medium
date: 2025-12-03
---

# Lab: Crack the Gate 2
## Vulnerability Overview
The target login system implemented a naive rate-limiting mechanism intended to block brute-force attacks by locking out IP addresses after repeated failed attempts. However, the system insecurely derived the client's source IP address from the user-controllable X-Forwarded-For HTTP header. This design flaw allowed an attacker to completely bypass the rate limit by spoofing a new source IP with each request, enabling a successful password brute-force attack.

## Vulnerable Endpoint
- POST /login (Primary authentication endpoint)

## Attack Flow
- Reconnaissance: Initial testing confirmed that multiple rapid failed login attempts from the same session resulted in a lockout message, confirming active rate limiting.
- Hypothesis: Based on the challenge description hinting at "trusting user-controlled headers," the X-Forwarded-For header was identified as the likely vector.
- Tool Setup:
    1. Burp Suite Intruder was used with Pitchfork attack type to iterate simultaneously through two payload sets: a list of candidate passwords and a list of unique IP addresses for spoofing.
    2. A Resource Pool was configured to throttle requests to 1 per second, ensuring the attack avoided potential secondary, request-rate-based limits and maintained stealth.
- Exploitation: The attack automated login requests for the known email ctf-player@picoctf.org. Each request claimed to originate from a different IP via the X-Forwarded-For header, tricking the rate-limiter into treating each attempt as coming from a new, unique user.
- Success: The brute-force process continued until a valid password from the provided list was matched, at which point the server responded with the successful login page containing the hidden flag.

## Exploitation Payload
The core exploit was the manipulation of the HTTP request header. The request structure sent by Burp Intruder was:
	`POST /login HTTP/1.1`
	`....`
	`X-Forwarded-For: <IP>`
	`{"email":"<given-email-by-lab>","password":"iauwdapjdoaipjuga"}`

## Payload Positions:
- §IP_ADDRESS§: A set of spoofed IP addresses `(e.g., 192.168.1.1, 192.168.1.2, 10.0.0.1)`.
- §PASSWORD§: The provided wordlist of potential passwords.

## Payload Breakdown

1. X-Forwarded-For Header: A standard HTTP header used by proxies to forward the original client IP address. When the application blindly trusts this value for rate-limiting decisions instead of the actual connection IP (TCP socket), it creates a critical logic flaw.

2. Pitchfork Attack Type: This Intruder mode is ideal for scenarios requiring synchronization between two payload sets. It ensures Request #1 uses Password #1 and IP #1, Request #2 uses Password #2 and IP #2, and so on, maintaining the one-to-one spoof relationship necessary for the bypass.

3. Resource Pool Throttling: Reducing the request rate to 1/second was a crucial adjustment. It demonstrated an understanding that while the primary IP-based limit was bypassed, the application might still have global or per-endpoint throughput limits that could hinder the attack if fired too aggressively.

## Exfiltrated Data
The successful login response contained the hidden secret (the flag), granting access to the protected system or revealing the challenge solution.

## Lesson Learned

- Never Trust User-Controlled Input for Security Decisions: This is a cardinal rule. Any security mechanism (rate limiting, authentication, authorization) that relies on client-supplied data (headers, cookies, form fields) can be trivially bypassed. Security decisions must be based on server-side, immutable data (like the actual connection socket information).

- Defense in Depth for Rate Limiting: Effective rate limiting should be multi-layered:
    1. Primary Layer: Based on the actual connection IP (which can be partially mitigated by botnets, making it insufficient alone).

    2. Secondary Layer: Based on session tokens or user account IDs post-authentication.

    3. Tertiary Layer: Behavioral analysis (e.g., speed of requests, mouse movements, puzzle challenges like CAPTCHA).

- The Importance of Attack Tuning: Your success hinged not just on the core bypass idea but on correctly tuning the attack tool (Resource Pool). Real-world systems often have multiple overlapping controls; effective exploitation requires adapting to these constraints.

## Remediation

1. Fix the Logic Flaw: The application's rate-limiting code must be modified to use the remote IP address provided by the web server or application framework `(e.g., REMOTE_ADDR in PHP, request.remote_ip in Rails)`, which is derived from the TCP connection and cannot be spoofed via HTTP headers.

2. Validate Proxy Setups: If the application is behind a trusted proxy or load balancer (which would set `X-Forwarded-For`), the server must be configured to only accept that header from the trusted proxy's IP address and then use the rightmost trusted IP in the chain.

3. Implement Token-Based Buckets: Introduce a second factor for rate limiting after the first failed attempt, such as requiring a newly issued, single-use token (sent via email or displayed on-screen) for subsequent attempts, moving the attack surface away from IP-based trust.
