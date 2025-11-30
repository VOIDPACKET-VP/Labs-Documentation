---
vulnerability: JWT Manipulation
platform: 247CTF
difficulty: Medium
date: 2025-11-16
---

# Lab: JWT Authentication Bypass
- Date: 2025-11-16
- Platform: 247CTF
- Difficulty: Moderate
- Vulnerability: JWT Weak Secret & Authentication Bypass

## Key Steps
- Reconnaissance: Analyzed the Flask application source code and identified JWT authentication mechanism
- Identify Vulnerability: Found that JWT validation checks for identity == 'admin' to reveal the flag
- Secret Cracking: Used jwt_tool to crack the weak JWT secret key (wepwn247)
- Token Forgery: Created a valid JWT token with identity set to "admin" using the cracked secret
- Authentication Bypass: Replaced the cookie value with the forged admin token to access the flag

## Tools Used
1. JWT_TOOL
2. Browser Developer Tools

## Payload
- Crack JWT secret
```python3 jwt_tool.py <jwt_token> -C -d /usr/share/wordlists/rockyou.txt```
- Forge admin token
```python3 jwt_tool.py <jwt_token (optional)> -T -S hs256 -p "wepwn247"```

## Lesson Learned
- Always use strong, unpredictable secrets for JWT signing
- JWT tokens should be treated as sensitive credentials
- Weak secrets can be easily cracked with offline tools
- The @jwt_optional decorator can lead to authentication bypass if not properly validated
- Regular secret rotation and strong key management are essential for JWT security