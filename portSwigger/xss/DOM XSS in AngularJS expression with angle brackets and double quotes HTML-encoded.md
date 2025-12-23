---
platform: PortSwigger
vulnerability: XSS
difficulty: Easy
date: 2025-12-22
---
# Description
-  This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within the search functionality.

- AngularJS is a popular JavaScript library, which scans the contents of HTML nodes containing the ng-app attribute (also known as an AngularJS directive). When a directive is added to the HTML code, you can execute JavaScript expressions within double curly braces. This technique is useful when angle brackets are being encoded.

- To solve this lab, perform a cross-site scripting attack that executes an AngularJS expression and calls the alert function. 

# Steps
1. In the source code we can see the `ng-app` attribute in the `<body>` tag : `<body ng-app>`
2. *AngularJS*'s syntax is executed between `{{}}`, so our payload has to be inside them
3. There is an event available on the `$scope` object in AngularJS called : `$on`, this event has a property : `.constructor()` which allows access to the Function constructor in JavaScript. Invoking it with a string argument can execute that string as code.
4. When user input reaches the `$on` event, an attacker can execute arbitrary code via that `constructor` property
5. All we have left to do now is craft the payload : `{{$on.constructor('alert(VP)')()}}`
# Mitigation
1. **AngularJS 1.x sandbox is fundamentally broken** - upgrade is the only real fix
2. **Never interpolate untrusted data** - use `ng-bind` instead of `{{ }}`
3. **Implement defense in depth** - client and server validation
4. **Use CSP headers** to limit script execution
5. **Sanitize all user input** before displaying