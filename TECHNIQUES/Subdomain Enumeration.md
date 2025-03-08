# Subdomain Enumeration


### Subdomain Enumeration

**Main Idea:** Find all the subdomains of a site to spot more weak spots.

**What It Is:**  
- Hunting for hidden subdomains (e.g., `shop.example.com`, `admin.example.com`) under a main domain (`example.com`).

**Why Do It:**  
- More subdomains = bigger attack surface.  
- Each one might have bugs to exploit.

**Example:**  
- For `example.com`, find `login.example.com`—maybe it’s got a weak login form.

**Remembering Tip:** Think of it as “mapping a website’s family tree”—find all the cousins with secrets!

---


### SSL/TLS Certificates OSINT

**Main Idea:** Use SSL/TLS certificate logs to find subdomains.

**What’s Going On:**  
- CAs (Certificate Authorities) log every SSL/TLS cert in public Certificate Transparency (CT) logs.  
- Logs show all certs made for a domain—past and present.

**How It Helps:**  
- Sites like `https://crt.sh` let you search logs for subdomains (e.g., `shop.example.com`).  

**Example:**  
- Search `example.com` on `crt.sh`—find `admin.example.com` you didn’t know about.

**Why It’s Cool:** Spots hidden subdomains that might be weak links.

**Remembering Tip:** Think of CT logs as a “domain’s guestbook”—everyone who got a cert signed in!

---


### Search Engines OSINT

**Main Idea:** Use search engines to hunt subdomains with smart filters.

**How It Works:**  
- Billions of sites indexed—perfect for finding subdomains.  
- Filter like `site:*.domain.com -site:www.domain.com` skips the main site, shows subs only.

**Example:**  
- Google `site:*.tryhackme.com -site:www.tryhackme.com`—might find `store.tryhackme.com`.

**Why It’s Cool:** Quick way to spot subdomains without guessing.

**Remembering Tip:** Think of it as “search engine binoculars”—zoom in on the domain’s hidden branches!

---


### DNS Bruteforce

**Main Idea:** Blast tons of subdomain guesses to find real ones fast.

**What It Is:**  
- Try heaps of common subdomains (e.g., `shop`, `admin`) from a list.  
- Automation tools handle the flood of DNS checks.

**Example:**  
- Tool guesses `shop.example.com`, `admin.example.com`—hits `login.example.com`.

**Why It’s Cool:** Finds subdomains manually guessing would miss.

**Remembering Tip:** Think of it as “DNS shotgun”—spray guesses, see what sticks!

---


### Sublist3r OSINT

**Main Idea:** Use Sublist3r to snag subdomains from a domain fast.

**What It Is:**  
- A Python tool that digs up subdomains using OSINT (e.g., search engines, cert logs).  

**Example:**  
- Run `sublist3r -d example.com`—finds `shop.example.com`, `admin.example.com`.

**Why It’s Cool:** Grabs subdomains from public sources without brute-forcing.

**Remembering Tip:** Think of Sublist3r as a “subdomain vacuum”—sucks up hidden names from the web!

---



### Virtual Hosts Discovery

**Main Idea:** Find hidden subdomains on a server using the Host header.

**What’s Going On:**  
- Some subdomains (e.g., dev or admin) aren’t in public DNS—kept private or in `/etc/hosts`.  
- Web servers use the Host header to pick the right site—tweak it to find secret ones.

**Example (Acme IT Support):**  
- On AttackBox, run:  
  `ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP`  
- Tons of hits—filter with `-fs {size}` (e.g., most common page size from first run).  
- Finds new subs like `dev.acmeitsupport.thm`.

**Why It’s Cool:** Uncovers stuff DNS misses by tricking the server.

**Remembering Tip:** Think of it as “knocking on server doors”—Host header’s the key, wordlist’s the guest list!

