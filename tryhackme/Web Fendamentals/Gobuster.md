# dir

| Flag | Long Flag     | Description                               |
| ---- | ------------- | ----------------------------------------- |
| -t   | --threads     | Number of concurrent threads (default 10) |
| -v   | --verbose     | Verbose output                            |
| -z   | --no-progress | Don't display progress                    |
| -q   | --quiet       | Don't print the banner and other noise    |
| -o   | --output      | Output file to write results to           |
### flags
| Flag | Long Flag                | Description                                                 |
| ---- | ------------------------ | ----------------------------------------------------------- |
| -c   | --cookies                | Cookies to use for requests                                 |
| -x   | --extensions             | File extension(s) to search for                             |
| -H   | --headers                | Specify HTTP headers, -H 'Header1: val1' -H 'Header2: val2' |
| -k   | --no-tls-validation      | Skip TLS certificate verification                           |
| -n   | --no-status              | Don't print status codes                                    |
| -P   | --password               | Password for Basic Auth                                     |
| -s   | --status-codes           | Positive status codes                                       |
| -b   | --status-codes-blacklist | Negative status codes                                       |
| -U   | --username               | Username for Basic Auth                                     |
`gobuster dir -u http://10.10.252.123/myfolder -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x.html,.css,.js`

### -k flag
- if HTTPS is enabled, may be cert error, use this flag
# dns
`gobuster dns -d mydomain.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`

| Flag | Long Flag    | Description                                                  |
| ---- | ------------ | ------------------------------------------------------------ |
| -c   | --show-cname | Show CNAME Records (cannot be used with '-i' option)         |
| -i   | --show-ips   | Show IP Addresses                                            |
| -r   | --resolver   | Use custom DNS server (format server.com or server.com:port) |