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

---
---

### HTTP and HTTPS: Key Notes  

#### **1. HTTP (HyperText Transfer Protocol)**  
- Developed by Tim Berners-Lee (1989-1991).  
- A protocol used for communication between a web browser and web server.  
- Transmits webpage data like HTML, images, videos, etc.  

#### **2. HTTPS (HyperText Transfer Protocol Secure)**  
- A secure version of HTTP.  
- Encrypts data, ensuring privacy and verifying the server's authenticity.  


### **3. URL (Uniform Resource Locator)**  
A URL is an instruction to access a resource on the internet. Its components:  
- **Scheme**: Protocol to use (e.g., HTTP, HTTPS, FTP).  
- **User**: Username and password (optional, for services requiring authentication).  
- **Host**: Domain name or IP address of the server.  
- **Port**: Default ports: 80 (HTTP), 443 (HTTPS). Other ports range from 1-65535.  
- **Path**: Location of the requested resource.  
- **Query String**: Additional data sent to the resource, e.g., `/blog?id=1`.  
- **Fragment**: Points to a specific section of a webpage, e.g., `#task3`.  


### **4. Making HTTP Requests**  
**Example Request**:  
```plaintext
GET / HTTP/1.1  
Host: tryhackme.com  
User-Agent: Mozilla/5.0 Firefox/87.0  
Referer: https://tryhackme.com/  
(blank line indicates end of request)
```  

- **GET / HTTP/1.1**: Requests the home page using HTTP version 1.1.  
- **Host**: Specifies the website (e.g., `tryhackme.com`).  
- **User-Agent**: Identifies the browser and version (e.g., Firefox 87).  
- **Referer**: Specifies the page that referred the request.  

**Example Response**:  
```plaintext
HTTP/1.1 200 OK  
Server: nginx/1.15.8  
Date: Fri, 09 Apr 2021 13:34:03 GMT  
Content-Type: text/html  
Content-Length: 98  

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```  

- **HTTP/1.1 200 OK**: Protocol version and status code.  
- **Server**: Web server software and version.  
- **Date**: Current server time and timezone.  
- **Content-Type**: Type of data (e.g., `text/html`).  
- **Content-Length**: Length of the response.  
- Blank line indicates end of headers.  
- Body contains the requested webpage content.  


### **5. Common HTTP Methods**  
- **GET**: Retrieve information from the server.  
- **POST**: Send data to the server (e.g., form submission).  
- **PUT**: Update existing information on the server.  
- **DELETE**: Remove information from the server.  


### **6. HTTP Status Codes**  
Status codes inform clients about the outcome of their requests:  

| **Code Range** | **Meaning**                        | **Common Codes**                              |  
|----------------|------------------------------------|-----------------------------------------------|  
| 100-199        | Informational (e.g., Continue).    | *Rarely used*.                               |  
| 200-299        | Success                           | `200 OK`, `201 Created`.                     |  
| 300-399        | Redirection                       | `301 Moved Permanently`, `302 Found`.        |  
| 400-499        | Client Errors                    | `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`. |  
| 500-599        | Server Errors                    | `500 Internal Server Error`, `503 Service Unavailable`. |  


### **7. HTTP Headers**  
#### **Common Request Headers**  
- **Host**: Specifies which website is being requested.  
- **User-Agent**: Browser and version information.  
- **Content-Length**: Length of data sent (e.g., in form submissions).  
- **Accept-Encoding**: Supported compression methods for data transfer.  
- **Cookie**: Sends stored data to the server.  

#### **Common Response Headers**  
- **Set-Cookie**: Stores information in the browser for future requests.  
- **Cache-Control**: Time for storing the response in the cache.  
- **Content-Type**: Indicates the type of response data (e.g., HTML, JSON).  
- **Content-Encoding**: Specifies compression used for data transfer.  

---
---

### Key Notes on Websites, Frontend, and Backend  

#### **Website Basics**  
- A website is made up of two major components:  
  1. **Front End (Client-Side):** How the browser displays the site.  
  2. **Back End (Server-Side):** Handles requests and sends responses.  

- Browsers send **requests** to a web server, which processes and returns **responses** to render pages.  

#### **Core Web Technologies**  
- **HTML (HyperText Markup Language):**  
  - Builds the structure of the website.  
  - Common elements:  
    - `<html>`: Root element.  
    - `<head>`: Contains metadata and the page title.  
    - `<body>`: Main content displayed in the browser.  
    - `<h1>`: Headings.  
    - `<p>`: Paragraphs.  
  - **Attributes:**  
    - `class`: Applies styling (can be shared by multiple elements).  
    - `id`: Unique identifier for an element.  
    - `src`: Specifies resource location, e.g., for images or scripts.  
  - View HTML source: Right-click > "View Page Source."

- **CSS (Cascading Style Sheets):** Styles the page to make it visually appealing.  

- **JavaScript (JS):**  
  - Adds interactivity and dynamic functionality.  
  - Executes through `<script>` tags, inline or external sources.  
  - Example:  
    ```javascript
    document.getElementById("demo").innerHTML = "Hack the Planet";
    ```  
  - HTML **events** like `onclick` and `onhover` can trigger JavaScript functions.  

#### **Common Security Issues in Web Development**  

1. **Sensitive Data Exposure:**  
   - Developers may accidentally leave sensitive data (e.g., credentials or private links) in the source code.  
   - **First Step in Security Testing:** Always check page source code for exposed sensitive information.

2. **HTML Injection:**  
   - Occurs when a website fails to sanitise user input, allowing malicious HTML or JavaScript to be injected into the page.  
   - **Example Attack:**  
     - Inputting `<h1>Hacked!</h1>` into an unfiltered field can alter the page appearance.  
   - **Prevention:**  
     - Always sanitise user input to remove malicious tags.  
     - Never trust user-provided data.

#### **Key Takeaways for Security Assessments**  
- Understand the structure of websites (frontend vs backend).  
- Review source code for potential sensitive information leaks.  
- Test input fields for injection vulnerabilities (e.g., HTML Injection).  
- Ensure robust input sanitisation to mitigate common vulnerabilities.





## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
