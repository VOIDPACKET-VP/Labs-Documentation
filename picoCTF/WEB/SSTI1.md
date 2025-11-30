---
vulnerability: SSTI
platform: picoCTF
difficulty: Easy
date: 2025-11-19
---
# Lab: Flask/Jinja2 SSTI Challenge
- Date: 2025-19-11
- Platform: picoCTF
- Difficulty: Easy
- Vulnerability: Server-Side Template Injection (SSTI)

## Key Steps
- Vulnerability Identification: Found SSTI vulnerability in the web application
- Template Engine Confirmation: Verified Jinja2 template engine using {{7*7}}
- Direct File Access: Used Flask's built-in get_flashed_messages function to access Python built-ins
- Flag Extraction: Read the flag file directly using open().read()

## Payload
```
{{ get_flashed_messages.__globals__.__builtins__.open("flag").read() }}
```

## Why It Worked
- ```get_flashed_messages``` is a Flask function available in all templates
- ```__globals__``` provides access to the function's global namespace
- ```__builtins__``` contains Python's built-in functions including open()
- The flag file was named ```"flag"``` in the current directory

## Lesson Learned
- Flask's template context contains useful built-in functions that can be exploited
- get_flashed_messages, config, request, lipsum are all potential entry points
- Sometimes the simplest path is the most effective - no need for complex class traversal
- Knowing framework-specific objects can lead to quicker exploitation