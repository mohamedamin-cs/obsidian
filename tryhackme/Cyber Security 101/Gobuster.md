h- **Content Management System ([[CMS]])** :These web applications are used to manage content on a website. For example, blogs, news sites, e-commerce sites and more!****
- **Enumeration** : Enumeration is the act of listing all the available resources.
- **Brute Force** : Brute force is the act of trying every possibility until a match is found. 
- gobuster --help
- A CNAME (Canonical Name) is a type of DNS (Domain Name System) record :
	- - If you have `www.example.com` and `blog.example.com`, instead of pointing both to the same IP address, you can make `blog.example.com` a CNAME to `www.example.com`.
	- Any changes to the IP of `www.example.com` automatically apply to `blog.example.com` as well.
- **examples** : ```gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js```
- `gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`
- `gobuster vhost -u "http://10.10.47.188" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320`
### DNS cheat-notes (TLD / SLD / subdomain)

- **TLD (Top-Level Domain):** rightmost label, e.g. `com`, `org`, `uk`.
    
- **SLD (Second-Level Domain):** label left of TLD — the registrable name, e.g. `example` in `example.com`.
    
- **eTLD / public suffix:** multi-label TLDs like `co.uk` or `github.io` (registrations occur under this).
    
- **Registrable domain (eTLD+1):** the purchasable domain, e.g. `example.co.uk`.
    
- **Subdomain:** any label left of the registrable domain (e.g. `shop` in `shop.example.com`).
    
- **Hostname / FQDN:** hostname + domain, e.g. `www.example.com` (fully qualified: `www.example.com.`).
    
- **Zone / authoritative NS:** a DNS zone holds records (A, AAAA, CNAME, MX, PTR, etc.) and is served by authoritative nameservers.
    
- **Tip:** read DNS names **right → left**; use `dig`, `host`, or `whois` to inspect parts.
uk (TLD)
└── co.uk (eTLD / public suffix)
    └── example.co.uk (registrable domain / eTLD+1)
        └── shop.example.co.uk (subdomain level 2)
            └── blog.shop.example.co.uk (subdomain level 1 / FQDN)