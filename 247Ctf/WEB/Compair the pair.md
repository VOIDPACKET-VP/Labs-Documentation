# CTF: PHP Type Juggling with Magic Hashes
- Date: 2025-11-16
- Platform: 247CTF
- Difficulty: Medium
- Vulnerability: PHP Type Juggling / Magic Hash Attack

## Challenge Overview
The challenge presented a PHP authentication system that uses MD5 hashing with a salt, but employs loose comparison (==) instead of strict comparison (===), allowing for type juggling attacks.

## Vulnerability Details
PHP's loose comparison interprets strings starting with "0e" as scientific notation (0 × 10^N = 0). If both the stored hash and the computed hash evaluate to 0, the comparison passes regardless of the actual hash values.

## Key Code Flaw
// VULNERABLE CODE:
```
if(isset($_GET['password']) && md5($salt . $_GET['password']) == $password_hash)
```

## Solution
Found input az038r where:
md5("f789bbc328a3d1a3az038r") = "0e69127414249092301303890256443"
Both hashes evaluate to 0 in PHP, granting access.
The script used to find the input can be found in my Scripts repo > "Scripts/Used_for_CTFs" under the name > "md5_salt.py"

## Payload
http://web195/?password=az038r

## Lesson Learned
- Never use loose comparison (==) for security-critical operations
- Always use strict comparison (===) or hash_equals() in PHP
- Magic hashes exist for MD5 and other algorithms
- Salts don't prevent type juggling attacks

## Prevention
```
if(md5($salt . $_GET['password']) === $password_hash)
// OR
if(hash_equals(md5($salt . $_GET['password']), $password_hash))
```