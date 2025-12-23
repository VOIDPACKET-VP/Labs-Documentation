---
platform: PortSwigger
vulnerability: XSS
difficulty: Easy
date: 2025-12-23
---
# Description
- This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. A script on the page then processes the reflected data in an unsafe way, ultimately writing it to a dangerous sink.

- To solve this lab, create an injection that calls the alert() function. 

# Steps
1. If we view the debugger in the DevTools we can see a file called `searchResults.js`
2. We can see how our input is being treated : `{"searchTerm":"test", "results":[]}`
3. We can notice with some testing that `"` are being escaped using `\` but `\` are not being escaped, also in JS `\\` becomes `\`
4. The payload is : `\"-alert(VP)}//`, the first `\` is used to cancel the escaping of the `"` (it becomes > `\\` = `\` ) ,we used the `-` to separate the expressions before the `alert() function` is called, the `}` used to close the JSON, and the `//` to comment out the rest
# Mitigation
1. Never use eval() with untrusted data - This is the root cause
2. JSON escaping must be complete - Escaping quotes but not backslashes creates vulnerability
3. Use JSON.parse() instead of eval() for JSON