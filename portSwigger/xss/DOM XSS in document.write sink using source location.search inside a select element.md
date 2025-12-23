---
platform: PortSwigger
vulnerability: XSS
difficulty: Easy
date: 2025-12-22
---
# Description
-  This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search which you can control using the website URL. The data is enclosed within a select element.

- To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function.

# Steps
1. With BURP intercept the traffic of the `check stock` functionality of any `product` (`/product` endpoint )
2. When we view the response, we can see some dangerous JS code :
	- The code checks if there is a `storeId` query in the `search` 
	- If there is : it closes the `input` with  `</select>`  
3. So we can take advantage of this and pop an alert box :
	- In the URL we add `&storeId=</select>;<script>alert(VP)</script>` 
	- The `</select>;` closes the HTML tag.
	- The `<script>alert(VP)</script>` executes, which gives us an Alert Box.

# Mitigation
1. **Never trust user input** - validate on server and client
2. **Escape output** - encode special characters before rendering
3. **Use safe DOM methods** - `textContent` over `innerHTML`
4. **Avoid `document.write()`** - it's inherently dangerous
5. **Implement CSP** - adds an extra layer of protection
