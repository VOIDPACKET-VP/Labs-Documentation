# Lab: Twig Template Injection with Character Filter Bypass
- Date: 2025-21-11
- Platform: 247CTF
- Difficulty: Medium
- Vulnerability: Server-Side Template Injection (SSTI) in Twig with Character Filter Bypass

## Lab Description
    This challenge involved exploiting a Twig template injection vulnerability where user input was filtered through a restrictive regular expression. The goal was to access the flag stored in the $_SERVER array's APP_FLAG variable.

## Key Steps
- Code Analysis: Identified the vulnerable /inject endpoint with character filtering
- Filter Understanding: Recognized the regex /[^{\.}a-z\|\_]/ only allowed {, }, ., |, _, and lowercase letters
- Twig Object Research: Discovered Symfony's app.request.server provides access to $_SERVER array
- Filter Bypass: Used allowed characters to construct Twig payloads
- Flag Extraction: Successfully retrieved the APP_FLAG value from server variables

## Vulnerable Endpoint
```
GET /inject?inject={{PAYLOAD}}
```

## Character Filter Restrictions
- The regex /[^{\.}a-z\|\_]/ only permitted:
    - { } . | _ (special characters)
    - a-z (lowercase letters)
    - Blocked: uppercase letters, numbers, most symbols, spaces

## Exploitation Payloads

    - Initial reconnaissance - dump all server variables
        /inject?inject={{app.request.server.all|json_encode|raw}}

    - Direct flag extraction (working payload)
        /inject?inject={{app.request.server.get('APP_FLAG')}}

    - Alternative extraction methods
        /inject?inject={{app.request.server.all.APP_FLAG}}

## Attack Flow
```Endpoint Discovery → Filter Analysis → Twig Object Research → 
Character-Compatible Payload Design → Flag Extraction
```

## Vulnerability Details
- Unsafe Template Construction: User input directly interpolated into Twig template
- Insufficient Filtering: Regex blacklist missed critical Twig syntax and object access patterns
- Symfony Framework Exposure: app.request.server object accessible through Twig context
- Server Information Disclosure: Full $_SERVER array accessible through template injection

## Twig-Specific Exploitation
- Object Access: app.request.server provides Symfony's server variable access
- Method Chaining: get('APP_FLAG') method call using allowed characters
- Filter Usage: json_encode|raw filters worked within character constraints
- Context Awareness: Twig in Symfony context exposes framework objects

## Technical Challenges Overcome
1. Character Restrictions: Built working payloads using only allowed characters
2. Case Sensitivity: Used lowercase method names within Twig syntax
3. Object Discovery: Identified accessible Symfony objects within Twig context
4. Flag Location: Located flag in $_SERVER['APP_FLAG'] rather than filesystem

## Lesson Learned
- Character blacklists are insufficient for template injection protection
- Framework context exposes additional attack vectors beyond standard template objects
- $_SERVER array can contain sensitive application data including flags
- Twig in Symfony provides extensive object access through app global variable
- Even restrictive filters can be bypassed with knowledge of available objects

## Remediation
- Use whitelist-based input validation instead of blacklists
- Avoid direct user input in template construction
- Implement context-aware output encoding
- Restrict template engine access to framework objects
- Store sensitive data outside of web-accessible arrays

# Real-World Impact: 
```This vulnerability demonstrates how inadequate input filtering combined with framework object exposure can lead to sensitive information disclosure in PHP applications using Symfony and Twig templates.```