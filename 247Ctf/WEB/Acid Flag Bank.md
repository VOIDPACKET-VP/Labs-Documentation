---
vulnerability: Race Condition
platform: 247CTF
difficulty: Medium
date: 2025-11-19
---

# Lab: Race Condition & Type Juggling in Banking System
- Date: 2025-19-11
- Platform: 247CTF
- Difficulty: Medium
- Vulnerability: Race Condition (TOCTOU) & PHP Type Juggling

## Key Steps
- Code Analysis: Identified the banking system with user funds transfer functionality
- Requirements Analysis: Flag requires >247 funds, but maximum transfer is 247
- Vulnerability Discovery: Found two potential attack vectors:
  - PHP type juggling in clean() function
  - Race condition in transfer logic
- Race Condition Exploitation: Sent 12 parallel transfer requests using Burp Repeater
- Flag Extraction: Used the inflated funds to purchase the flag

## Race Condition Attack (Burp Repeater Method)
```GET /?from=1&to=2&amount=247 HTTP/1.1```

## Attack Process:
- Intercept a transfer request in Burp
- Send to Repeater
- Create multiple Repeater tabs with the same request
- Select all tabs and click "Send group" (parallel execution)
- Repeat process 3-4 times with 12 concurrent requests each

- Result: User 2 funds increased from 0 to 741 through concurrent transfers.

## Type Juggling Payloads (Alternative)
```
?from=2&to=1&amount=247e0     # Scientific notation
?from=2&to=1&amount=247.0000000000001  # Float precision
?from=2&to=1&amount=247abc    # String truncation
```
## Why The Vulnerabilities Exist
1. Race Condition (TOCTOU)
    ```
    if ($db->validUser($to) && $db->validUser($from) && 
        $db->getFunds($from) >= $amount) {
        $db->updateFunds($from, $db->getFunds($from) - $amount);
        $db->updateFunds($to, $db->getFunds($to) + $amount);
    }
    ```
    - The Problem:
        - Checks funds (getFunds()) then updates (updateFunds()) separately
        - No database transactions or locking
        - Multiple requests can read the same balance before any updates occur
    - The Fix:
        ```
        // Use database transactions
        $this->pdo->exec('BEGIN TRANSACTION');
        // Perform both operations
        $this->pdo->exec('COMMIT');
        ```
2. PHP Type Juggling
    ```
    public function clean($x)
    {
        return round((int)trim($x));
    }
    ```
    - The Problem:
        - (int)"247e0" = 247 (scientific notation converted)
        - (int)"247.0000000000001" = 247 (float truncated)
        - round() can cause precision issues with large numbers
        - No validation that input is actually an integer

    - The Fix:
        ```
        public function clean($x)
        {
            if (!is_numeric($x) || strpos($x, '.') !== false) {
                return 0;
            }
            return (int)$x;
        }
        ```

## Lesson Learned
- Race conditions occur when check and use operations aren't atomic
- Burp Repeater is perfect for concurrent request testing
- PHP's weak typing requires strict input validation
- Financial operations must use database transactions
- Parallel execution can create application state violations