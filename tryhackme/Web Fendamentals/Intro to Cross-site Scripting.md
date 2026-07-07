document  contain user's session token : document.cookie
**Proof Of Concept** : alert() : simplest of payloads where all you want to do is demonstrate that you can achieve XSS on a website
- The `fetch` function sends an HTTP request to an external server (`hacker.thm`)
- A ***keylogger*** (short for "keystroke logger") is a type of surveillance technology—either software or hardware—designed to record every single key you press on a keyboard.
- **Reflected XSS** happens when user-supplied data in an HTTP request is included in the webpage source without any validation.
- **Stored XSS :** the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the site or web page. 
- **Blind XSS** : A website has a contact form where you can message a member of staff. The message content doesn't get checked for any malicious code, which allows the attacker to enter anything they wish. These messages then get turned into support tickets which staff view on a private web portal. **popular tool:** https://github.com/mandatoryprogrammer/xsshunter-express
- **/images/cat.jpg" onload="alert('THM');**

----
In the world of bug bounty hunting, JavaScript is less about "making things pretty" and more about **finding where data is handled poorly.** Think of a website like a building: JavaScript is the plumbing. If you can find a pipe that leaks user input into a dangerous place, you’ve found a bug. Here are the most important functions and methods to look for.

---

### 1. The "Sources" (Where the Leak Starts)

These are properties that allow a user to influence the script. When you see these in source code, an attacker likely controls the data inside them.

- **`location.search`**: Everything after the `?` in a URL (e.g., `?id=123`).
    
- **`location.hash`**: Everything after the `#` in a URL. This is a "favorite" for DOM-based XSS because hashes are often not sent to the server, so server-side firewalls miss them.
    
- **`document.referrer`**: The URL of the page the user came from.
    
- **`window.name`**: A property that persists even when you navigate to a different page—often used to bypass data limits.
    

---

### 2. The "Dangerous Sinks" (Where the Explosion Happens)

A "Sink" is a function that can execute or render the data it receives. If a **Source** flows into one of these **Sinks** without being cleaned, you have a vulnerability.

|**Method**|**Why it's Dangerous**|**Potential Bug**|
|---|---|---|
|**`.innerHTML`**|It renders strings as HTML. If I put `<img src=x onerror=alert(1)>` in here, it executes.|**DOM XSS**|
|**`eval()`**|It takes a string and runs it as raw JavaScript code. Never use this.|**Remote Code Execution**|
|**`setTimeout()`**|Like `eval`, if the first argument is a string, it will execute that string.|**Logic Flaws / XSS**|
|**`document.write()`**|Writes directly to the page. Very old, very vulnerable.|**XSS**|

---

### 3. Navigation & Redirection

Attackers love finding "Open Redirects." This is when a script takes a URL from a user and sends them there automatically.

- **`window.location.href = ...`**
    
- **`window.location.replace(...)`**
    

**The Bug:** If you see `window.location.href = params.get("return_url")`, you can change the URL to `https://malicious-site.com`. Users trust the original site but end up on yours.

---

### 4. Communication Methods

Modern sites (Single Page Applications) use these to talk to the "Backend." As a hunter, you want to see _what_ they are sending.

- **`fetch()`**: The modern way to send/receive data.
    
- **`XMLHttpRequest` (XHR)**: The older way, but still everywhere.
    
- **`postMessage()`**: This allows different windows (like an iframe and a main page) to talk to each other.
    
    > **Pro Tip:** If a site uses `postMessage` but doesn't check _who_ sent the message (`event.origin`), you can send a malicious message from your own site to steal their data.
    

---

### 5. Data Handling

- **`JSON.parse()`**: Converts a string into a JS object. If handled poorly, it can lead to **Prototype Pollution**.
    
- **`atob()` / `btoa()`**: These handle Base64. If you see a weird string like `YWRtaW4=`, try `atob('YWRtaW4=')` in your console—it might reveal a hidden username or ID (in this case, "admin").
    

---

### Summary for your "Cheat Sheet"

When you are looking at a JavaScript file in your browser's **Sources** tab (F12), use `Ctrl + F` to search for these specific strings:

1. `.innerHTML`
    
2. `eval()`
    
3. `postMessage`
    
4. `location.hash`
    
5. `document.cookie`
    

**Would you like me to show you a real-world example of how a hunter "connects the dots" from a `location.hash` source to an `innerHTML` sink?**