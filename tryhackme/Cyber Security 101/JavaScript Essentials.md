js is **interpreted** = the code is executed in the browser (no compiling)
js is executed in the client side

#### internal JS
```javascript
 <!DOCTYPE html>
<html lang="en">
<head>
    <title>Internal JS</title>
</head>
<body>
    <h1>Addition of Two Numbers</h1>
    <p id="result"></p>

    <script>
        let x = 5;
        let y = 10;
        let result = x + y;
        document.getElementById("result").innerHTML = "The result is: " + result;
    </script>
</body>
</html>
```

#### external JS
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>External JS</title>
</head>
<body>
    <h1>Addition of Two Numbers</h1>
    <p id="result"></p>

    <!-- Link to the external JS file -->
    <script src="script.js"></script>
</body>
</html>
```

## abusing dialogue messages
- `alert("Hello THM")`
- prompt will display a dialogue box : 
```javascript
name = prompt("What is your name?");
    alert("Hello " + name);
```
- `confirm` : ok/cancel
#### Exploring minified files
 - ***Minification*** in JS is the process of compressing JS files by removing all unnecessary characters(spaces, line breaks, comments, and even shortening variable names)
 - ***obfuscation*** is often used to make JS harder to understand by adding undesired code, renaming variables and functions to meaningless names, and even inserting dummy code.
 - js obfuscator : https://codebeautify.org/javascript-obfuscator
 - js debofusscator : https://obf-io.deobfuscate.io/

---
### small javascript  course:

## 1. The DOM (Document Object Model)

The DOM is how JavaScript "sees" the HTML page. For a bug hunter, the DOM is a map of potential attack vectors.

- **`document.cookie`**: Often the "Holy Grail." If you can access this via XSS, you can steal sessions.
    
- **`document.location`**: Contains the URL. Attackers look here for parameters they can manipulate.
    
- **`document.write()`**: A dangerous function that writes directly to the page—prime for XSS.
    

---

## 2. Sources vs. Sinks

This is the most important concept in web security.

- **The Source:** Where user-controlled input starts (e.g., `location.search`, `location.hash`, `window.name`).
    
- **The Sink:** The "dangerous" function where that input ends up (e.g., `eval()`, `setTimeout()`, `.innerHTML`).
    

| **Source (Input)** | **Sink (Execution)** | **Potential Vulnerability** |
| ------------------ | -------------------- | --------------------------- |
| `location.hash`    | `innerHTML`          | DOM-based XSS               |
| `location.search`  | `window.location`    | Open Redirect               |
| `JSON.parse`       | Object property      | Prototype Pollution         |

---

## 3. Asynchronous JS (Fetch & Promises)

Modern sites use `fetch()` to send data in the background. As a hunter, you need to watch these "XHR" requests in your browser's Network tab.

JavaScript

```
// Example of a background data leak
fetch('/api/user/settings')
  .then(response => response.json())
  .then(data => {
    console.log(data); // If this data contains PII, it's a bug!
  });
```

---

## 4. Local Storage & Session Storage

Websites often store sensitive data (like JWT tokens or API keys) in the browser's storage rather than cookies.

- **`localStorage.getItem('token')`**: Persistent data.
    
- **`sessionStorage.getItem('session')`**: Clears when the tab closes.
    

> **Security Tip:** If a site stores a sensitive token in `localStorage` and has an XSS vulnerability, you can grab that token with one line of JS: `alert(localStorage.getItem('key'))`.

---

## 5. Prototype Pollution (Advanced)

This is a "trendy" bug. JavaScript uses **Prototypes** to share methods between objects. If you can "pollute" the base object, you can change the behavior of the entire application.
s
JavaScript

```
// The "Poison"
let user_input = JSON.parse('{"__proto__": {"isAdmin": true}}');
Object.assign({}, user_input); 

// The Result
let regular_user = {};
console.log(regular_user.isAdmin); // Outputs: true!
```

---

### How to Practice

1. **Read the Source:** Right-click any site -> "Inspect" -> "Sources" tab. Look for `.js` files.
    
2. **Use the Console:** Open your dev tools (F12) and type `window`. Look at all the objects available to you.
    
3. **Search for Keywords:** In the source code, use `Ctrl+Shift+F` to search for "sinks" like `.innerHTML` or `eval(`.
    

**Would you like me to give you a list of "Dangerous Sinks" to search for when you're auditing a website's JavaScript files?**