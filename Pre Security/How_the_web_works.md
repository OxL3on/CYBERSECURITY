### DNS (Domain Name System): Key Notes  

#### **1. Purpose of DNS**  
- Translates human-readable domain names (e.g., `tryhackme.com`) into IP addresses (e.g., `104.26.10.229`) for communication.  
- Simplifies access to websites by avoiding the need to remember complex IP addresses.  

#### **2. Domain Hierarchy**  
- **Root Domain**: The starting point of the DNS hierarchy.  
- **TLD (Top-Level Domain)**:  
  - Example: `.com`, `.org`, `.edu`.  
  - **Types**:  
    - **gTLD (Generic TLD)**: Represents purpose, e.g., `.com` (commercial), `.org` (organization).  
    - **ccTLD (Country Code TLD)**: Represents geographic regions, e.g., `.ca` (Canada), `.co.uk` (UK).  
- **Second-Level Domain**:  
  - Example: In `tryhackme.com`, `tryhackme` is the second-level domain.  
- **Subdomain**:  
  - Example: `admin.tryhackme.com`, where `admin` is the subdomain.  
  - Can include multiple levels, e.g., `jupiter.servers.tryhackme.com`.  

#### **3. Common DNS Record Types**  
- **A Record**: Resolves to an IPv4 address (e.g., `104.26.10.229`).  
- **AAAA Record**: Resolves to an IPv6 address (e.g., `2606:4700:20::681a:be5`).  
- **CNAME Record**: Resolves to another domain (e.g., `store.tryhackme.com` -> `shops.shopify.com`).  
- **MX Record**: Points to mail servers for handling email (includes priority for fallback servers).  
- **TXT Record**: Free text field used for:  
  - Verifying domain ownership.  
  - Specifying authorized email servers to prevent spam.  

#### **4. How DNS Works**  
1. **Local Cache Check**:  
   - Computer checks if the domain has been recently queried.  
2. **Recursive DNS Server**:  
   - Provided by ISP or configured manually.  
   - Checks its cache; if not found, forwards the query.  
3. **Root DNS Servers**:  
   - Redirect query to the appropriate TLD server (e.g., `.com`).  
4. **TLD Server**:  
   - Provides the location of the authoritative nameserver for the domain.  
5. **Authoritative DNS Server**:  
   - Stores the actual DNS records for the domain.  
   - Sends the requested DNS record back to the Recursive DNS Server.  
6. **Cache and Relay**:  
   - Recursive server caches the response for future use and sends it to the client.  

#### **5. TTL (Time To Live)**  
- Specifies how long a DNS response can be cached locally before it must be re-queried.  
- Helps reduce DNS traffic and improve response times.  

### **Applications in Ethical Hacking**  
- **DNS Reconnaissance**: Identify subdomains and misconfigured DNS records.  
- **Exploiting DNS Records**: Analyze A, CNAME, and TXT records for vulnerabilities.  
- **DNS Cache Poisoning**: Redirect traffic to malicious servers by altering cached DNS responses.






## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
