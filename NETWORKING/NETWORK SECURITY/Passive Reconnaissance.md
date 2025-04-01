# Passive Reconnaissance


**Passive vs. Active Recon**

1. **What’s Recon?**
   - It’s gathering info about a target before attacking or defending.
   - Tip: Like scouting an enemy camp in a game.

2. **Passive Recon**
   - Sneaky info collection using public stuff—no touching the target.
   - Examples: Checking DNS records, job ads, or news about a company.
   - Tip: It’s like spying from a hill with binoculars.

3. **Active Recon**
   - Direct poking at the target—less sneaky, more hands-on.
   - Examples: Connecting to servers (HTTP, FTP), calling the company, or sneaking in.
   - Tip: Like knocking on doors to test locks.

4. **Key Difference**
   - Passive = quiet and legal; Active = loud and risky (needs permission).
   - Tip: Passive watches, Active touches.

---
---


**Whois**

1. **What’s Whois?**
   - A tool to get info about a domain name (e.g., who owns it, when it was made).
   - Tip: Like a phonebook for websites.

2. **Key Info You Get**
   - Registrar: Who sold the domain (e.g., Namecheap).
   - Contact: Owner’s name, address, phone (if not hidden).
   - Dates: Created, updated, expires (e.g., tryhackme.com: 2018-2027).
   - Name Server: Which server handles the domain’s DNS.
   - Tip: It’s a treasure map of domain details.

3. **How to Use It**
   - On Linux (e.g., Kali), type: `whois domain` in terminal.
   - Online services work too, but terminal’s faster.

4. **Example Output**
   - `whois tryhackme.com` shows Namecheap as registrar, creation date (2018), and more.
   - Privacy services might hide owner info.

5. **Why It Matters**
   - Helps find attack points (e.g., email or DNS servers) for testing.
   - Tip: Spies use it to plan; defenders use it to hide.

---
---


