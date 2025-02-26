# Firewall Fundamentals



### Purpose of a Firewall

**Main Idea:** A firewall is like a digital security guard that checks all traffic (data) going in and out of your device or network to keep bad stuff out.

**Why It’s Needed:**  
- Tons of data flows between devices and the internet daily.  
- Without a guard, sneaky intruders could slip in unnoticed.  

**What It Does:**  
- Watches incoming and outgoing traffic.  
- Uses rules you set (like “no strangers allowed!”) to allow or block data.  
- Stops unauthorized access, just like a guard at a mall entrance.  

**Bonus:** Modern firewalls do more than just rule-checking—they add extra protection layers.  

**Remembering Trick:** Think of a firewall as a bouncer at a club, checking IDs (rules) to decide who gets in or out!

---


### Types of Firewalls

**Main Idea:** Firewalls come in different flavors, each doing a special job to block bad traffic at different OSI layers.

**Common Types:**  
1. **Stateless Firewall** (Layer 3 & 4)  
   - Checks packets with rules but forgets past connections.  
   - Fast but dumb—treats every packet like it’s new.  
   - *Example:* Blocks a shady source, then forgets and checks it again later.

2. **Stateful Firewall** (Layer 3 & 4)  
   - Remembers past connections in a “state table.”  
   - Smarter—allows or blocks based on history.  
   - *Example:* Lets a good connection keep going without rechecking every packet.

3. **Proxy Firewall** (Layer 7)  
   - Middleman that hides your network and checks packet contents.  
   - Filters based on what’s inside (like blocking bad websites).  
   - *Tip:* Think of it as a spy swapping your ID for safety.

4. **Next-Generation Firewall (NGFW)** (Layer 3-7)  
   - Super smart—deep checks, blocks threats live, decrypts SSL/TLS.  
   - Uses patterns and threat intel to stop attacks.  
   - *Example:* Spots and stops a sneaky hack instantly.

**Quick Cheat Sheet:**  
- **Stateless:** Fast, forgets.  
- **Stateful:** Remembers, tracks.  
- **Proxy:** Hides, digs into content.  
- **NGFW:** Advanced, all-in-one protector.

**Remembering Trick:** Picture firewalls as guards—Stateless is forgetful, Stateful has a notebook, Proxy checks your bags, and NGFW is a high-tech robot guard!

---


### Rules in Firewalls

**Main Idea:** Firewall rules let you control what traffic gets in or out of your network by setting custom instructions.

**Rule Basics:**  
- **Source:** Where traffic starts (IP address).  
- **Destination:** Where it’s going (IP address).  
- **Port:** Which “door” it uses (like 80 for web).  
- **Protocol:** How it talks (like TCP).  
- **Action:** What to do (allow, deny, forward).  
- **Direction:** In, out, or rerouted.

**Actions Explained:**  
1. **Allow:** Lets traffic through.  
   - *Example:* Allow outgoing web traffic (port 80) from 192.168.1.0/24.  
2. **Deny:** Blocks traffic.  
   - *Example:* Deny incoming SSH (port 22) to 192.168.1.0/24.  
3. **Forward:** Sends traffic somewhere else.  
   - *Example:* Forward incoming web traffic (port 80) to 192.168.1.8.

**Rule Directions:**  
- **Inbound:** For stuff coming in (like allowing web traffic to a server).  
- **Outbound:** For stuff going out (like blocking email from most devices).  
- **Forward:** Reroutes traffic inside (like sending web requests to a server).

**Remembering Trick:** Think of rules as a traffic cop—telling cars (data) where to go, stop, or turn based on their “license plate” (IP) and “road” (port)!

---


### Linux iptables Firewall

**Main Idea:** Linux has built-in firewall tools to control network traffic, with Netfilter as the core system.

**Key Tools:**  
1. **Netfilter:** The backbone for Linux firewalls—handles filtering, NAT, and tracking.  
2. **iptables:** Most popular tool, uses Netfilter to set traffic rules.  
3. **nftables:** Newer, fancier version of iptables.  
4. **firewalld:** Comes with ready-made zones and rules.  
5. **ufw:** Simple interface for beginners to manage iptables rules.

**Basic ufw Commands:**  
- **Check status:** `sudo ufw status` (Is it on or off?)  
- **Turn on:** `sudo ufw enable` (Activates firewall).  
- **Allow all outgoing:** `sudo ufw default allow outgoing` (Lets all outbound traffic go unless blocked).  
- **Deny SSH in:** `sudo ufw deny 22/tcp` (Blocks incoming SSH on port 22).  
- **List rules:** `sudo ufw status numbered` (Shows all active rules).  
- **Delete rule:** `sudo ufw delete 2` (Removes rule #2).  

**Why It Matters:** These tools let you decide what traffic to allow or block, keeping your Linux system safe.

**Remembering Trick:** Think of ufw as a friendly gatekeeper making iptables rules easy—like giving simple orders to a smart guard dog (Netfilter)!

---


### Windows Defender Firewall

**Main Idea:** Windows Defender Firewall is a built-in tool to control network traffic on your Windows system.

**How to Start:**  
- Search “Windows Defender Firewall” in the Windows search bar to open it.  
- Main dashboard shows network profiles and options.

**Network Profiles:**  
1. **Private:** Rules for trusted home networks.  
2. **Public:** Rules for untrusted places (like coffee shops)—can block all incoming traffic.  
- *Tip:* Toggle apps on/off for each profile via “Allow an app” (option 1).  
- Turn it on/off (option 2) or reset to defaults (option 3).

**Custom Rules:**  
- Go to “Advanced Settings” to make your own rules.  
- *Example Rule:* Block outgoing HTTP (port 80) and HTTPS (port 443):  
  - Pick “Custom” > “All programs” > TCP, ports 80,443 > “Block” > Apply to all profiles > Name it.  
  - Test: Can’t visit websites (like http://10.10.10.10/) after blocking.

**Why It Matters:** Lets you allow or block specific traffic (like web browsing) for safety.

**Remembering Trick:** Think of it as a gatekeeper for your Windows “house”—you set rules to lock out unwanted guests (traffic)!

