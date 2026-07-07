g - ***def :*** SSRF stands for Server-Side Request Forgery. It's a vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the resource of the attacker's choosing.
![[img/Pasted image 20251228183212.png]]
![[img/Pasted image 20251228183230.png]]
![[img/Pasted image 20251228183246.png]]
![[img/Pasted image 20251228183333.png]]
### SSRF Bypasses & Filtering
---
#### 🛡️ Deny List (Blacklisting)

- **Concept**: Permissive by default; blocks specific "known bad" inputs (e.g., `localhost`, `127.0.0.1`).
    
- **Cloud Targets**: Often used to block `169.254.169.254` (AWS/GCP/Azure Metadata API).
    
- **Bypass Techniques**:
    
    - **Alternative IP Formats**:
        
        - **Decimal**: `2130706433`
            
        - **Octal**: `017700000001`
            
        - **Shortened**: `127.1` or `0`
            
    - **DNS Pinning/Resolvers**: Use a domain (like `127.0.0.1.nip.io`) or a custom subdomain that resolves to a denied IP.
        

#### ✅ Allow List (Whitelisting)

- **Concept**: Restrictive by default; only allows inputs that match a strict pattern (e.g., `https://trusted.thm`).
    
- **Bypass Technique**:
    
    - **Subdomain Manipulation**: If the logic only checks if the URL _starts_ with the trusted string, use: `https://trusted.thm.attacker-domain.com`.
        
    - **URL Parsing Quirks**: Using `@` symbols or path confusion to trick the parser.
        

#### 🔀 Open Redirect

- **Concept**: A legitimate site feature that redirects users (e.g., `/redirect?url=...`).
    
- **SSRF Utility**: If the SSRF filter is too strict to bypass directly, point the SSRF at a **local** open redirect.
    
- **Execution**:
    
    1. Request: `SSRF_Param=https://website.thm/redirect?url=http://169.254.169.254`
        
    2. The server validates the URL as "safe" (it's its own domain).
        
    3. The server fetches the page, follows the redirect, and inadvertently hits the sensitive metadata IP.