# Passive Reconnaissance


### **Passive vs. Active Recon**

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


### **nslookup and dig**

1. **What Are nslookup and dig?**
   - Tools to find a domain’s IP addresses and other info (like email servers).
   - Tip: They’re like detectives for domain details.

2. **Using nslookup**
   - Command: `nslookup [OPTIONS] DOMAIN_NAME [SERVER]`
   - Options: `-type=A` for IPv4, `-type=AAAA` for IPv6, `-type=MX` for mail servers, etc.
   - Example: `nslookup -type=A tryhackme.com 1.1.1.1` shows IPv4 addresses.
   - Tip: Pick a DNS server (e.g., 1.1.1.1, 8.8.8.8) to ask.

3. **Key Query Types**
   - A: IPv4 addresses (e.g., tryhackme.com has 172.67.69.208).
   - AAAA: IPv6 addresses.
   - MX: Mail servers (e.g., tryhackme.com uses Google’s mail servers).
   - Tip: MX shows where emails go—like finding the mailbox.

4. **Using dig**
   - More advanced than nslookup, shows extra details like TTL.
   - Command: `dig [SERVER] DOMAIN_NAME TYPE`
   - Example: `dig tryhackme.com MX` or `dig @1.1.1.1 tryhackme.com MX`.
   - Tip: dig digs deeper, nslookup is quicker.

5. **Why It Matters**
   - Helps find IPs or servers to test for weaknesses.
   - Tip: It’s like mapping the target’s digital neighborhood.

---
---




