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