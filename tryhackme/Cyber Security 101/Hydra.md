- ***Definition:*** Hydra is a brute force online password cracking program, a quick system login password “hacking” tool.
- **has the ability to brute force the following protocols:** “Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP, HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MEMCACHED, MONGODB, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, Radmin, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC and XMPP.”
- `hydra -l user -P passlist.txt ftp://10.10.186.250` : brute force ftp 
### ssh
- `hydra -l <username> -P <full path to pass> 10.10.186.250 -t 4 ssh`: (-l →login/ -P →list of passwords/ -t →number of threads to spawn).
### Post Web Form
- `sudo hydra <username> <wordlist> 10.10.186.250 http-post-form "<path>:<login_credentials>:<invalid_response>"`

|Option|Description|
|---|---|
|`-l`|the username for (web form) login|
|`-P`|the password list to use|
|`http-post-form`|the type of the form is POST|
|`<path>`|the login page URL, for example, `login.php`|
|`<login_credentials>`|the username and password used to log in, for example, `username=^USER^&password=^PASS^`|
|`<invalid_response>`|part of the response when the login fails|
|`-V`|verbose output for every attempt|
`hydra -l molly -P /root/Desktop/wordlists/rockyou.txt 10.10.186.250  http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" `
