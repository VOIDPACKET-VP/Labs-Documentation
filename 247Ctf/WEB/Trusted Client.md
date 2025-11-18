# CTF: Client-Side Authentication Bypass
** Platform: 247CTF
** Difficulty: Easy/Medium
** Vulnerability: Hardcoded Credentials in Client-Side Code

## Key Steps:
1. Identified client-side login form with obfuscated JavaScript

2. Recognized JSF*ck obfuscation pattern using only []()!+ characters

3. Used online JSF*ck decoder (dcode.fr) to de-obfuscate the code

4. Discovered hardcoded credentials containing the flag in plaintext

## Obfuscated Code Pattern:
The JavaScript was obfuscated using JSF*ck technique:

```
[0]] + "false"[2] + "true"[0] + "true"[3] + "true"[1]])[1 + [0]] + "true"[1]])[1 + [0]] + "true"[0] + "true"[1] + ([false] + [][[]])[1 + [0]] + ...
```
## De-obfuscated Code:
```
if (this.username.value == 'the_flag_is' && 
    this.password.value == '247CTF{6c91b7f7f12c852f892293d16dba0148}') {
    alert('Valid username and password!');
} else {
    alert('Invalid username and password!');
}
```
## Credentials Found:
Username: the_flag_is

Password/Flag: 247CTF{6c91b7f7f12c852f892293d16dba0148}

## Tools Used:
Browser Developer Tools - View source code

dcode.fr JSF*ck decoder - De-obfuscation

## Vulnerability Details:
- Storing authentication logic client-side allows anyone to view and bypass it

- JSF*ck obfuscation provides no real security - only obscurity

- Hardcoded secrets in client-side code are always accessible to users

- No server-side validation means client-side checks are meaningless

## Lesson Learned:
- Never store credentials or sensitive logic client-side

- Obfuscation ≠ Encryption - JSF*ck can be easily reversed

- Always validate authentication server-side

- Client-side checks are for UX, not security

- Assume users can see all client-side code

## Mitigation:
- Implement proper server-side authentication

- Use secure session management with HTTP-only cookies

- Never expose secrets in client-side code

- Treat client-side as completely untrusted