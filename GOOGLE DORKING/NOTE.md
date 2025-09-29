### `inurl:`
**Description**: Search for a value that is contained somewhere in the URL.  
**Example**:  
```bash
preventing ransomware inurl:fbi
```

### `site:`
**Description**: Search only within the specified website's domain.  
**Example**:  
```bash
windows xp end of life site:microsoft.com
```

### `filetype:`
**Description**: Search only for files, not webpages.  
**Example**:  
```bash
"nasa moon landing filetype:JPG"
```

### `allinurl:`
**Description**: Search all of the following words in the URL.  
**Example**:  
```bash
allinurl:"blog wordpress" information security
```

### `intext:`
**Description**: Search the body of the webpage for specific text.  
**Example**:  
```bash
patient record intext:"index of /htdocs"
```

### `related:`
**Description**: Find websites that are related to the search term.  
**Example**:  
```bash
related:sans.org
```

### `info:`
**Description**: Find supplemental information Google may have on this page (useful for finding cached pages).  
**Example**:  
```bash
info:www.usgs.gov
```

### `link:`
**Description**: Find other pages indexed by Google that reference this link.  
**Example**:  
```bash
link:http://www.somecompany.com/supersecretfile.doc
```

### `"quote"`
**Description**: Search for an exact phrase (though results may include related words).  
**Example**:  
```bash
"Malware Hunting"
```

### `+word`
**Description**: Show results with this word exactly. Do not include similar words.  
**Example**:  
```bash
Malware +Hunter
```

### `-word/query`
**Description**: Exclude this word from the search results.  
**Example**:  
```bash
Advanced Malware Hunting -beginner -introduction -site:microsoft.com
```

### `"word * word"`
**Description**: Use wildcard to search for anything between these two words, but include both.  
**Example**:  
```bash
"Next * Firewalls with *"
```

### `OR (or | )`
**Description**: Return results for either item. The pipe character `|` can be used in place of `OR`.  
**Example**:  
```bash
"locky OR ransomware"
"locky | ransomware"
```

### `AND (or &) `
**Description**: Return results that include both items. The ampersand `&` can be used in place of `AND`.  
**Example**:  
```bash
"cissp AND certification"
"cissp & certification"
```

---

### **Sensitive Data Exposure Dorks**

1. **Find exposed files with passwords:**
   ```
   inurl:"/etc/passwd"
   ```
   This dork can reveal publicly available password files in unsecured directories.

2. **Find exposed database dumps:**
   ```
   filetype:sql intext:"dump" inurl:"/db/"
   ```
   This dork helps locate exposed database dumps that may contain sensitive information.

3. **Find unsecured backup files:**
   ```
   filetype:bak inurl:"backup"
   ```
   Exposed backup files may contain sensitive data, such as website databases, files, and configuration information.

4. **Find config files with sensitive information:**
   ```
   inurl:"config" "password"
   ```
   Config files often contain sensitive credentials and keys.

5. **Search for exposed API keys or secrets:**
   ```
   inurl:"api_key" "secret"
   ```
   Exposed API keys in URLs or source code can lead to unauthorized access.

---

### **Vulnerable Websites Dorks**

1. **Find PHP source code exposed to the web:**
   ```
   inurl:"index.php" intext:"Warning: include"
   ```
   This can reveal PHP errors or misconfigurations that may lead to code injection vulnerabilities.

2. **Find websites with exposed directory listings:**
   ```
   intitle:"Index of /" inurl:"/admin/"
   ```
   Directory listings may expose files that shouldn't be publicly accessible.

3. **Find vulnerable WordPress sites:**
   ```
   inurl:"wp-content" "404 Not Found"
   ```
   This dork helps you locate WordPress sites that may be vulnerable to attacks like SQL Injection or Cross-Site Scripting (XSS).

4. **Search for potentially vulnerable FTP servers:**
   ```
   filetype:log inurl:"ftp" "failed login"
   ```
   This can help identify misconfigured FTP servers with login issues or previous failed login attempts.

---

### **Misconfigured Services Dorks**

1. **Find unsecured MongoDB instances:**
   ```
   inurl:"MongoDB" intext:"admin"
   ```
   This dork looks for unsecured MongoDB databases that may be exposed to the internet.

2. **Find exposed Redis instances:**
   ```
   inurl:"Redis" intext:"server started"
   ```
   Redis instances exposed without proper authentication could allow attackers to execute commands.

3. **Find exposed Elasticsearch indices:**
   ```
   inurl:"elasticsearch" intext:"cluster_name"
   ```
   Exposed Elasticsearch servers may allow attackers to search and query sensitive data.

4. **Search for unsecured Jenkins servers:**
   ```
   inurl:"/jenkins" "Admin Login"
   ```
   Jenkins servers exposed to the internet can be vulnerable to unauthorized access and misconfiguration.

---

### **Exploiting Web Vulnerabilities Dorks**

1. **Find servers with directory traversal vulnerabilities:**
   ```
   inurl:"..%2F..%2F" intitle:"index of"
   ```
   Directory traversal can reveal sensitive files from web servers.

2. **Search for XSS (Cross-Site Scripting) vulnerabilities in URLs:**
   ```
   inurl:"<script" "alert("
   ```
   This dork searches for vulnerable scripts that may be susceptible to XSS attacks.

3. **Find exposed files that might be used for remote code execution:**
   ```
   filetype:php inurl:"shell"
   ```
   Exposed PHP shells on websites could lead to remote code execution vulnerabilities.

4. **Find pages with SQL injection vulnerabilities:**
   ```
   inurl:"id=" "You have an error in your SQL syntax"
   ```
   This dork helps to locate pages where SQL injection may be possible based on error messages.

---

### **Social Engineering and Information Gathering Dorks**

1. **Find personal information about employees:**
   ```
   "email" "phone" "address" site:linkedin.com
   ```
   This dork helps gather publicly available information about individuals on LinkedIn.

2. **Search for sensitive documents like PDFs with personal details:**
   ```
   filetype:pdf intext:"contact us" "email"
   ```
   This dork looks for public PDF documents with contact information.

3. **Find exposed Google Docs containing private data:**
   ```
   filetype:pdf inurl:"docs.google.com" "confidential"
   ```
   Publicly shared Google Docs could contain sensitive or confidential information.

---
