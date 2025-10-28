### Broken Access controll
Simply put, broken access control allows attackers to bypass **authorisation**, allowing them to view sensitive data or perform tasks they aren't supposed to.
### Insecure Direct Object Reference
**[[IDOR]]** or **Insecure Direct Object Reference** refers to an access control vulnerability where you can access resources you wouldn't ordinarily be able to see.
![[img/Pasted image 20250928113311.png]]
### Cryptographic Failures
- databases can also be stored as files. These are referred to as "[[flat-file]]" databases
- format = SQLite database
- hese can be interacted with in most programming languages and have a dedicated client for querying them on the command line. This client is called `sqlite3`.
#### sqlite
- `sqlite3 example.db`
- `.table` : see tables 
- `PRAGMA table_info(customers);` to see the table information
### injection 
- These flaws occur because the application interprets user-controlled input as commands or parameters.(sql injection / command injection).
- to prevent this use : 
	- ***allow list*** : when input is sent to the server, this input is compared to a list of safe inputs or characters.
	- ***stripping input*** : If the input contains dangerous characters, these are removed before processing.
#### command injection
- https://www.php.net/manual/en/function.passthru.php
- ![[img/9f657b909062ac82af12548b4f346aec.png]]
### Security Misconfiguration
- occur when security could have been appropriately configured but was not.
- [[Werkzeug]]  a vital component in Python-based web applications as it provides an interface for web servers to execute the Python code (URL/console).
### Identification and Authentication Failures Practical
- developers forget to sanitise the input(username & password) given by the user in the code of their application
- We will enter " admin" without the quotes (notice the space at the start). Now when you enter that in the username field and enter other required information like email id or password and submit that data, it will register a new user, but that user will have the same right as the admin account
### Software Integrity Failures
-  include jQuery in your website directly from their servers↓↓↓
```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```

- an attacker somehow hacks into the jQuery official repository, they could change the contents of `https://code.jquery.com/jquery-3.6.1.min.js`
### Data Integrity Failures & JWTs
#### Cookies & Sessions
- Web apps use **cookies** to store session tokens.
- Cookies are sent with every request.
- **Problem:** If user tampers with cookie (e.g., changes username), server trusts it → **data integrity failure**.
#### [[JWT]] (JSON Web Token)
- Token that ensures **data integrity**.
- Signed by server using a secret key → tampering is detectable.
- Can store key-value pairs (e.g., username, expiry).
#### JWT Structure
1. **Header**: metadata + algorithm  
2. **Payload**: data (username, exp)  
3. **Signature**: server-generated, verifies payload integrity
![[img/Pasted image 20251016230419.png]]
#### Server-Side Request Forgery (SSRF)
- attacker can coerce a web application into sending requests on their behalf to arbitrary destinations while having control of the contents of the request itself.
![[img/271d0075650cdf6499f994f99fa7eb8a.png]]