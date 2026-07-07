low-privileged web user account: `www-data`
**MIME :** Multipurpose Internet Mail Extensions (MIME) is an Internet standard that extends the format of email messages to support text in character sets other than ASCII, as well as attachments of audio, video, images, and application programs.
![[img/Pasted image 20260313155212.png]]
**_Magic Number validation_** Magic numbers are the more accurate way of determining the contents of a file; although, they are by no means impossible to fake. The "magic number" of a file is a string of bytes at the very beginning of the file content which identify the content. For example, a PNG file would have these bytes at the very top of the file: `89 50 4E 47 0D 0A 1A 0A`.
___
# Filtering 
 `.php3`, `.php4`, `.php5`, `.php7`, `.phps`, `.php-s`, `.pht` and `.phar`. Many of these bypass the filter (which only blocks`.php` and `.phtml`)
# Magic numbers
**signature :** https://en.wikipedia.org/wiki/List_of_file_signatures
_note :_ use the Linux `file`
# 📑 File Upload Methodology (Black-Box)

## 🏁 Phase 1: Reconnaissance

- **Identify Tech Stack:**
    
    - Check `Wappalyzer` or HTTP Response Headers (`Server`, `X-Powered-By`).
        
    - _Goal:_ Determine if you need a `.php` (Apache), `.aspx` (IIS), or `.jsp` (Tomcat) payload.
        
- **Locate Upload Vector:** Search for profile picture updates, document uploads, or contact forms.
    
- **Client-Side Inspection:** * View Page Source (`Ctrl+U`) for JavaScript validation.
    
    - Look for `onchange` or `onsubmit` events that check file extensions before the upload starts.
        

---

## 🟢 Phase 2: Establishing a Baseline

1. **Upload an Innocent File:** Upload a valid `image.png` or `test.txt`.
    
2. **Locate the File:**
    
    - Check the response for a direct link.
        
    - Inspect the `<img>` tag `src` attribute if it's a profile pic.
        
    - **Gobuster:** If the path is hidden, run:
        
        `gobuster dir -u http://target.com -w /path/to/wordlist -x php,jpg,png`
        
3. **Analyze Naming Scheme:** Does the server keep the name `image.png`, or rename it to a hash like `a8f3...png`?
    

---

## 🛡️ Phase 3: Enumerating Server-Side Filters

If your shell is blocked, identify _why_ by testing one variable at a time:

|**Test Type**|**Action**|**Interpretation**|
|---|---|---|
|**Extension Filter**|Upload `test.invalid`|**Success:** Blacklist (Easy to bypass)<br><br>  <br><br>**Fail:** Whitelist (Harder)|
|**MIME Type**|Intercept in Burp; change `Content-Type: text/php` to `image/jpeg`|**Success:** Filter is only checking the Header.|
|**Magic Numbers**|Add `FF D8 FF DB` (JPEG) to the top of your PHP script.|**Success:** Server is inspecting file hex signatures.|
|**File Length**|Upload a 1MB file, then 5MB, etc.|Useful for finding limits that might break large reverse shells.|

---

## 🚀 Phase 4: Bypass Techniques

- **Extension Bypasses (Blacklist):**
    
    - Try alternatives: `.phtml`, `.php3`, `.php5`, `.phar`.
        
    - Try case sensitivity: `.PhP`, `.AsPx`.
        
- **Double Extensions:** `shell.jpg.php` or `shell.php.jpg`.
    
- **Null Byte Injection (Older Servers):** `shell.php%00.jpg`.
    
- **Config File Overwrite:** Upload a `.htaccess` file to allow execution in a specific directory.
    

---

## 🛠️ Handy Tools & Commands

> [!TIP]
> 
> **Gobuster Search for Uploaded Payloads:**
> 
> `gobuster dir -u http://TARGET_IP/uploads/ -w /usr/share/wordlists/dirb/common.txt -x php,txt,html`

> [!QUOTE]
> 
> **Magic Numbers Reference:**
> 
> - **PNG:** `89 50 4E 47 0D 0A 1A 0A`
>     
> - **JPG:** `FF D8 FF DB`
>     
> - **GIF:** `47 49 46 38 37 61` (Handy because you can just type `GIF87a;` at the start of a script).
>