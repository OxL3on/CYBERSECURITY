# IDS Fundamentals


### What Is an IDS

**Main Idea:** An Intrusion Detection System (IDS) watches network traffic inside to catch bad stuff that slips past the firewall.

**How It Works:**  
- Firewalls guard the “gate” (network edge), but IDS is like indoor security cameras.  
- It spots weird or harmful activity (using signatures or odd patterns) after a connection’s already in.  
- Alerts admins about trouble but doesn’t stop it itself.

**Why It Matters:**  
- Catches attackers who sneak by the firewall with legit-looking traffic.  
- Think of it as a “heads-up” for security teams.

**Remembering Trick:** Picture IDS as a quiet watchdog inside your network “house”—barking (alerting) when it sees trouble the gatekeeper (firewall) missed!

---


### Types of IDS 

**Main Idea:** IDS comes in different types based on where it’s placed and how it spots trouble.

**Deployment Types:**  
1. **HIDS (Host-Based):** Lives on one device, watches that device’s activity.  
   - Good detail, but tough to manage on lots of machines.  
2. **NIDS (Network-Based):** Sits in the network, watches all traffic.  
   - Sees everything, easier to manage centrally.

**Detection Types:**  
1. **Signature-Based:** Matches traffic to known attack “fingerprints” (signatures).  
   - Fast for old threats, misses new (zero-day) ones.  
   - *Example:* Snort uses this.  
2. **Anomaly-Based:** Learns “normal” behavior, flags anything weird.  
   - Catches new attacks but may cry wolf too much (false positives).  
3. **Hybrid:** Mixes both—uses signatures for known stuff, anomalies for new threats.

**Why It Matters:**  
- HIDS for deep host checks, NIDS for big-picture view.  
- Signature catches repeats, anomaly spots surprises, hybrid does both.

**Remembering Trick:** Think of IDS as detectives—HIDS guards one house, NIDS patrols the neighborhood, Signature checks mugshots, Anomaly spots odd behavior, Hybrid does it all!

---


### IDS Example: Snort

**Main Idea:** Snort is a free, popular IDS that spots threats using rules (signatures) and odd patterns.

**What It Does:**  
- Comes with built-in rules to catch known attacks.  
- You can tweak or add custom rules for specific traffic.  
- Started in 1998, still widely used.

**Modes of Snort:**  
1. **Packet Sniffer:** Just watches and shows traffic, no judging.  
   - *Use:* Troubleshooting network slowdowns.  
2. **Packet Logging:** Watches, detects, and saves traffic as PCAP files.  
   - *Use:* Forensic teams analyzing past attacks.  
3. **NIDS (Network IDS):** Main mode—scans traffic live, matches rules, and alerts on threats.  
   - *Use:* Real-time threat hunting.

**Why It Matters:** NIDS mode is the star for IDS, but other modes help with monitoring or investigations.

**Remembering Trick:** Think of Snort as a network “sniffer dog”—sniffing (watching), barking (alerting), or leaving tracks (logging) depending on the job!

---

### Snort Usage

**Main Idea:** Snort watches network traffic and alerts on threats using rules you set up.

**Setup Basics:**  
- Install Snort, set your network interface and range (e.g., promiscuous mode for whole network).  
- Key files in `/etc/snort`: `snort.conf` (settings) and `rules` folder (rule files).

**Rule Format:**  
- *Example:* `alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)`  
- Parts: Action (alert), Protocol (ICMP), Source/Dest (any/loopback), Ports (any), Message/SID/Rev (alert info).  

**Using Snort:**  
1. **Edit Rule:** Add to `/etc/snort/rules/local.rules` with `sudo nano`.  
   - Save with Ctrl+X, Y.  
2. **Run Snort:** `sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf`  
   - Watches loopback (lo), alerts to console.  
3. **Test Rule:** Ping `127.0.0.1`—see “Loopback Ping Detected” alert.  
4. **PCAP Analysis:** `sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf`  
   - Checks old traffic files for threats.

**Why It Matters:** Snort catches live or past intrusions with custom or built-in rules.

**Remembering Trick:** Think of Snort as a “snitch”—writing rules in its notebook (rules file) and shouting (alerting) when it catches ping “thieves”!

---


