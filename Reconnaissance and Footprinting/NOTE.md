# Reconnaissance Tools Cheatsheet

## **1. WAFW00f**
### **Purpose**:
Detects Web Application Firewalls (WAFs) on a website.

### **Basic Commands**:
- Detect WAF:
  ```bash
  wafw00f <target-url>
  ```
- Verbose output for detailed information:
  ```bash
  wafw00f -v <target-url>
  ```

### **Pro Tips**:
- Use detected WAF details to research bypass techniques.
- Combine with Burp Suite for custom payload testing.

---

## **2. host**
### **Purpose**:
Performs DNS lookups to retrieve domain records.

### **Basic Commands**:
- Retrieve A record:
  ```bash
  host <domain>
  ```
- Retrieve NS records:
  ```bash
  host -t ns <domain>
  ```
- Reverse DNS lookup:
  ```bash
  host <IP>
  ```

### **Pro Tips**:
- Look for subdomain misconfigurations or interesting services.

---

## **3. whois**
### **Purpose**:
Fetches domain registration and ownership details.

### **Basic Commands**:
- Basic WHOIS query:
  ```bash
  whois <domain>
  ```
- Query using a specific WHOIS server:
  ```bash
  whois -h <whois-server> <domain>
  ```

### **Pro Tips**:
- Check for emails or registrant details that could be leveraged for phishing.
- Use tools like **theHarvester** to automate email collection.

---

## **4. WhatWeb**
### **Purpose**:
Fingerprints web technologies (CMS, server, plugins, etc.).

### **Basic Commands**:
- Scan a single URL:
  ```bash
  whatweb <url>
  ```
- Enable aggressive mode for more information:
  ```bash
  whatweb -a 3 <url>
  ```
- Scan multiple URLs from a file:
  ```bash
  whatweb -i urls.txt
  ```

### **Pro Tips**:
- Match technologies with vulnerability databases to find exploits.

---

## **5. DNSRecon**
### **Purpose**:
Performs DNS enumeration and checks for vulnerabilities like zone transfers.

### **Basic Commands**:
- Retrieve all DNS records:
  ```bash
  dnsrecon -d <domain>
  ```
- Test for zone transfer vulnerabilities:
  ```bash
  dnsrecon -d <domain> -t axfr
  ```
- Perform reverse lookup for a range of IPs:
  ```bash
  dnsrecon -r <start-IP>-<end-IP>
  ```

### **Pro Tips**:
- Misconfigured DNS zone transfers can expose internal records.

---

## **6. Subfinder**
### **Purpose**:
Discovers subdomains of a domain.

### **Basic Commands**:
- Basic subdomain discovery:
  ```bash
  subfinder -d <domain>
  ```
- Output results to a file:
  ```bash
  subfinder -d <domain> -o subdomains.txt
  ```
- Use with passive sources only:
  ```bash
  subfinder -d <domain> -nW
  ```

### **Pro Tips**:
- Pipe results into other tools like **HTTPX** to find live hosts:
  ```bash
  cat subdomains.txt | httpx -silent
  ```

---

## **7. theHarvester**
### **Purpose**:
Gathers public information like emails, subdomains, and IPs.

### **Basic Commands**:
- Search with Bing:
  ```bash
  theHarvester -d <domain> -b bing
  ```
- Save output to a file:
  ```bash
  theHarvester -d <domain> -b bing -f output.html
  ```
- Use multiple sources:
  ```bash
  theHarvester -d <domain> -b google,shodan,bing
  ```

### **Pro Tips**:
- Configure API keys in `~/.theHarvester/api-keys.yaml` for more data.
- Combine results with other tools (e.g., Subfinder).

---

## **General Workflow**
1. **Discover Subdomains**:
   - Use **Subfinder** for initial discovery.
   - Verify live hosts with **HTTPX** or a similar tool.

2. **Enumerate DNS**:
   - Use **host** and **DNSRecon** to gather DNS records and identify misconfigurations.

3. **Fingerprint Technologies**:
   - Use **WhatWeb** to identify technologies and look for vulnerabilities.

4. **Check WAF Presence**:
   - Use **WAFW00f** to detect and research bypass techniques if necessary.

5. **Collect Public Information**:
   - Use **theHarvester** and **whois** to gather details about emails, registrants, and infrastructure.



---

## **Shodan**  
- **Purpose**: Search engine for Internet-connected devices (servers, routers, IoT devices).  
- **Use Cases**: Identify device types, versions, and geographic distribution (e.g., search for `apache 2.4.1`).  
- **Additional Resources**:  
  - Explore **Shodan Search Query Examples** for insights.  
  - Use **Shodan Trends** (subscription required) for historical data analysis.  

---

## **Censys**  
- **Purpose**: Search engine for Internet-connected assets (hosts, websites, certificates).  
- **Focus**: Enumerates domains, audits ports/services, and discovers rogue assets.  
- **Use Cases**: Investigate domains, monitor certificates, and map Internet-facing infrastructure.  
- **Resource**: Check **Censys Search Use Cases** for detailed examples.  

---

## **VirusTotal**  
- **Purpose**: Scans files/URLs with multiple antivirus engines for malware.  
- **Features**:  
  - Upload files, URLs, or file hashes for analysis.  
  - View community comments for contextual insights.  
  - Detection might occasionally yield false positives.  
- **Output**: Displays results from multiple antivirus engines in a single operation.  

---

## **Have I Been Pwned (HIBP)**  
- **Purpose**: Checks if an email address appears in leaked data breaches.  
- **Significance**: Reveals compromised private information and passwords.  
- **Concern**: Reused passwords across platforms increase risk if one platform is breached.  

---

## **Vulnerabilities and Exploits**  

### **CVE (Common Vulnerabilities and Exposures)**  
- **Purpose**: A standardized dictionary of vulnerabilities.  
- **Format**: Unique identifiers like `CVE-2024-29988`.  
- **Maintained By**: MITRE Corporation.  
- **Resources**:  
  - **CVE Program Website**  
  - **National Vulnerability Database (NVD)**  

### **Exploit Database**  
- **Purpose**: Repository of exploit codes for vulnerabilities (e.g., Penetration testing).  
- **Features**:  
  - Contains exploit codes from various authors, some verified.  
  - Exploit use requires permission (e.g., via legally binding agreements).  
- **Additional Resource**:  
  - **GitHub**: Hosts PoC, exploit tools, and scripts related to CVEs.  

---  
