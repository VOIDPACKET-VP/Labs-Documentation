---
vulnerability: Info Disclosure
platform: picoCTF
difficulty: Easy
date: 2025-11-19
---
# Lab: Information Disclosure Chain - Web Configuration Files
- Date: 2025-19-11
- Platform: picoCTF
- Difficulty: Easy
- Vulnerability: Information Disclosure via Exposed Configuration Files

## Key Steps
- Source Code Analysis: Found suspicious JavaScript comment about search engine indexing
- HTML Source Inspection: Discovered first flag part in HTML comments
- CSS File Examination: Found second flag part in CSS file comments
- Robots.txt Access: Accessed /robots.txt revealing:
    - Third flag part: t_0f_pl4c
    - Apache server hint pointing to .htaccess
- .htaccess Discovery: Found fourth flag part: 3s_2_lO0k and macOS hint
- .DS_Store Access: Retrieved final flag parts from macOS metadata file

## Flag Parts Location
- Part 1: HTML source code comments
- Part 2: CSS file comments
- Part 3: /robots.txt file
- Part 4: /.htaccess file
- Final Parts: /.DS_Store file

## Complete Flag
```picoCTF{th4t_0f_pl4c3s_2_lO0k_[rest_of_flag]}```

## Exploitation Path
```JavaScript Comment → HTML Source → CSS File → robots.txt → .htaccess → .DS_Store ```

## Vulnerabilities Exploited
- Exposed configuration files (robots.txt, .htaccess)
- Developer comments in source code
- macOS metadata file (.DS_Store) exposure
- Poor information hygiene in production environment

## Lesson Learned
- Never leave configuration files publicly accessible
- Remove developer comments from production code
- Disable serving of system files like .DS_Store
- Information disclosure chains can reveal complete application secrets
- Every exposed file becomes a potential attack vector

## Real-World Impact: 
```This exact vulnerability chain has exposed admin panels, API keys, and sensitive paths in real web applications, leading to full system compromise.```