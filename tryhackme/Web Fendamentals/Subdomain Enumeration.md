##  OSINT: Certificate Transparency (CT)
- **CT Logs:** Public ledgers of every SSL/TLS certificate issued by CAs.
    
- **Goal:** Prevent fraud and accidental mis-issuance.
    
- **OSINT Use:** Discovering subdomains (e.g., `dev.target.com`, `internal.target.com`) passively.
    
https://crt.sh/ :  A searchable database of these public logs.

## OSINT: Search Engine Dorking

- **Concept:** Using advanced search filters (Google Dorks) to find indexed subdomains.
    
- **Filter:** `site:*.domain.com` (finds all subdomains).
    
- **Exclusion:** `-site:www.domain.com` (removes the main site to find "hidden" ones).
    
- **Benefit:** Discovers pages that have been crawled/indexed by search bots.