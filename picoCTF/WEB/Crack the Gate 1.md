# Lab: Source Code Analysis & Header Manipulation
- Date: 2025-11-16
- Platform: picoCTF
- Difficulty: Easy
- Vulnerability: Information Disclosure & Authorization Bypass

## Key Steps
- Source Code Analysis: Examined the webpage source code and discovered a hidden note in the comments
- Decode the Hint: The note was encoded using ROT13 cipher - "ABGR:" decodes to "NOTE:"
- Extract Instructions: Decoded the full message revealing authentication requirements
- Header Manipulation: Added the required X-Dev-Access: yes HTTP header to bypass authentication
- Flag Retrieval: Accessed the protected resource using the custom header to obtain the flag

## Payload
1. Using Burp repeater : add ```X-Dev-Access: yes``` to the request.
2. Using curl : ``` curl -H "X-Dev-Access: yes" http://target-url/ ```

## Lesson Learned
- Always inspect source code and comments for hidden information
- Common encodings like ROT13 are frequently used in CTF challenges
- Custom HTTP headers can be used for authentication/authorization bypass
- Developer comments sometimes contain sensitive information or hints
- The phrase "technical class" in the note suggests this was an educational example about header-based access control
