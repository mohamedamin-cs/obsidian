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
   