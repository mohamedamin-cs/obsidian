S- Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and a web server.
- Burp Suite is frequently used when attacking web applications and ______ mobile applications.
### Core tools
- **Proxy**: Intercepts and modifies HTTP requests/responses. 
- **Repeater**: Resend modified requests for testing (e.g., SQLi). 
- **Intruder**: Automates request spraying (rate-limited). 
- **Decoder**: Encodes/decodes data for payload crafting. 
- **Comparer**: Compares data at word/byte level via shortcut. 
- **Sequencer**: Analyzes token randomness (e.g., session cookies).
![[img/11202e4c73faa30a757f1439b63b85c6.png]]

| Shortcut           | Tab          |
| ------------------ | ------------ |
| `Ctrl + Shift + D` | Dashboard    |
| `Ctrl + Shift + T` | Target tab   |
| `Ctrl + Shift + P` | Proxy tab    |
| `Ctrl + Shift + I` | Intruder tab |
| `Ctrl + Shift + R` | Repeater tab |
### Scoping and Targeting
- we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) we want to test.
- in **target** : right click -> add to scope
- in settings : proxy -> response interception rule ->  And Url / Or request was intercepted / intercept response based on the following rules