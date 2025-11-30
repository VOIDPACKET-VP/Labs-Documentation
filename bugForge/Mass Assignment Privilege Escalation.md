---
vulnerability: Mass Assignment
platform: BugForge
difficulty: Easy
date: 2025-11-10
---
# CTF: Mass Assignment Privilege Escalation

**Date:** 2025-11-10 
**Platform:** BugForge.io 
**Difficulty:** Easy  
**Vulnerability:** Mass assignment

## Key Steps
1. Intercepted the registration request using Burp Suite and observed a role parameter in the JSON payload.
2. Modified the request by changing username/email and adding "role": "admin" to the registration object.
3. Successfully created an administrator account, logged in, and accessed the admin panel to retrieve the flag.

## Payload
{
  "username": "voidpacket_admin",
  "email": "void@packet.com",
  "role": "admin"
}

## Lesson learned
Mass assignment vulnerabilities occur when applications automatically bind user-supplied parameters to object properties without proper filtering. Even parameters not visible in the UI can be manipulated if they're part of the expected data model. Always implement parameter whitelisting on server-side and never trust that clients will only send "allowed" fields.

