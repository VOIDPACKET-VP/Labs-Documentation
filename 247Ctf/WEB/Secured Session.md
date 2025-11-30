---
vulnerability: Info Disclosure
platform: 247CTF
difficulty: Medium
date: 2025-11-18
---
# CTF: Flask Session Information Disclosure

**Platform: 247CTF
**Difficulty: Medium
**Vulnerability: Information Disclosure via Session Cookie

## Key Steps:
1.Discovered /flag endpoint from source code exposure at /

2.Accessed /flag endpoint which set a session cookie containing the flag

3.Decoded Flask session cookie using base64 decoding

4.Extracted the double-base64 encoded flag from session data

5.Decoded the inner base64 to reveal the flag

## Flask Session Structure:
Flask sessions use the format: base64(data).timestamp.signature

-base64(data): The actual session data, base64-encoded (often compressed)

-timestamp: Session creation timestamp

-signature: HMAC signature to prevent tampering

## Critical Insight:
While the signature prevents modification of the session, it does not prevent reading the session contents. Any sensitive data stored in the session is exposed to clients.

## Payload:
```
# Original session cookie:
# eyJmbGFnIjp7IiBiIjoiTWpRM1ExUkdlMlJoT0RBM09UVm1PR0UxWTJGaU1tVXdNemRrTnpNNE5UZ3dOMkk1WVRreGZRPT0ifX0.Zl7j8A.2vJ8eR3vVnHk9pLm1qT4wX7bCy0g

# Step 1: Decode the base64 data portion
session_data = "eyJmbGFnIjp7IiBiIjoiTWpRM1ExUkdlMlJoT0RBM09UVm1PR0UxWTJGaU1tVXdNemRrTnpNNE5UZ3dOMkk1WVRreGZRPT0ifX0"
decoded = base64.b64decode(session_data)
# Returns: {"flag":{" b":"MjQ3Q1RGe2RhODA3OTVmOGE1Y2FiMmUwMzdkNzM4NTgwN2I5YTkxfQ=="}}

# Step 2: Decode the inner base64 flag
flag_encoded = "MjQ3Q1RGe2RhODA3OTVmOGE1Y2FiMmUwMzdkNzM4NTgwN2I5YTkxfQ=="
flag = base64.b64decode(flag_encoded).decode()
# Returns: 247CTF{......}
```
## Lesson Learned:
1.Never store sensitive data in client-side sessions, even if signed

2.Sessions are for non-sensitive user data only - not secrets, keys, or flags

3.The signature protects integrity but not confidentiality - data is still readable by clients

4.Always validate what you're exposing in source code and error messages

## Tools Used:
-Burp Suite: For endpoint discovery and session cookie extraction

-Base64 decoding: Either via Burp Decoder or Python for complex nested encoding

