# Lab: Cookie Enumeration & IDOR Vulnerability
- Date: 2025-19-11
- Platform: picoCTF
- Difficulty: Easy
- Vulnerability: Insecure Direct Object Reference (IDOR) via Cookie Manipulation

## Key Steps
- Traffic Analysis: Used Firefox Developer Tools to analyze application flow
- Application Understanding: Discovered the search → redirect → cookie validation pattern
- Cookie Behavior Discovery: Found that different cookie names mapped to numeric IDs
- Vulnerability Identification: Recognized IDOR vulnerability in cookie-based access control
- Automated Enumeration: Wrote Python script to brute-force all possible cookie values

## Application Flow Analysis
```
User Input → POST /search → Redirect → GET /check → Cookie Validation → Custom Message
```
## The Vulnerability
- Each cookie/biscuit type was assigned a sequential numeric ID in the cookie
- The application used cookie value name={id} to retrieve messages
- No authorization checks - any number could access any message
- Flag was hidden in one of the numeric ID responses

## Exploitation Script
```
#!/bin/python3
import requests

for i in range(25):
    cookie = 'name={}'.format(i)
    headers = {'Cookie': cookie}
    
    r = requests.get('http://mercury.picoctf.net:<port>/check', headers=headers)
    if (r.status_code == 200) and ('picoCTF' in r.text):
        print(r.text)
```
## Attack Methodology
- Cookie Value Brute Force: Tested numeric IDs from 0-24
- Response Filtering: Checked for flag pattern in responses
- Automated Discovery: Found flag in one of the numeric ID responses

## Why It Worked
- Insecure Direct Object Reference (IDOR): Direct access to objects via predictable identifiers
- Lack of Session Validation: No user authentication tied to cookie values
- Predictable Identifier Pattern: Sequential numeric IDs easily enumerable

## Lesson Learned
- Never use predictable identifiers for sensitive data access
- Implement proper session management and authorization checks
- Validate user permissions for every object access request
- Sequential IDs are easily enumerable - use random UUIDs instead
- Cookie values should be encrypted or signed to prevent tampering

## Remediation
- Implement user authentication and session management
- Use random, non-sequential identifiers for objects
- Add authorization checks for all object access
- Sign or encrypt cookies to prevent manipulation
- Implement rate limiting to prevent enumeration

## Real-World Impact: 
```IDOR vulnerabilities regularly expose sensitive user data, including personal information, financial records, and private messages in production applications.```

# NOTE :
    I WASN'T SUCCESSFUL TO SOLVE THIS LAB, SO I AHD TO CHECK SOMEONE ELSE'S DOCUMENTATION, HERE IS THE LINK > ```https://cyb3rwhitesnake.medium.com/picoctf-cookies-web-39d8fedd345f```