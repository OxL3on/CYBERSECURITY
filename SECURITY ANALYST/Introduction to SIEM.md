# Introduction to SIEM



### What is SIEM
SIEM stands for Security Information and Event Management system. It is a tool that collects data from various endpoints/network devices across the network, stores them at a centralized place, and performs correlation on them. This room will cover the basic concepts required to understand SIEM and how it works.



### Network Visibility with SIEM

**Main Idea:** SIEM helps you see everything happening in a network so you can spot and fix problems fast.

**Why It Matters:**  
- Networks have stuff like computers (Endpoints), servers, and websites talking to each other or the internet via a router.  
- Every piece makes logs (records of what’s happening), but checking them one by one is slow and hard.

**Two Types of Logs:**  
1. **Host Logs** (Stuff on a device):  
   - Examples: A user opens a file, logs in, or runs a program.  
   - Tools: Windows Event Logs, Sysmon.  
   - *Tip:* Think of it like a diary of what’s happening inside your computer.

2. **Network Logs** (Stuff between devices):  
   - Examples: SSH login, downloading a file via FTP, browsing a website.  
   - *Tip:* Imagine it as tracking messages sent between houses.

**SIEM’s Superpowers:**  
- Collects all logs instantly.  
- Spots weird stuff (like an alert for “Hey, something’s fishy!”).  
- Watches everything 24/7.  
- Helps dig into old problems or stop new threats.  
- Shows data in cool visuals.  

**Remembering Trick:** Picture SIEM as a superhero guard watching your network city, catching bad guys by reading everyone’s diaries and messages!


---

### Log Sources & Log Ingestion

**Main Idea:** Devices in a network make logs (records) of what’s happening, and SIEM grabs them to keep an eye on things.

**Common Log Sources:**  
1. **Windows Machine**  
   - Logs: User logins, events (seen in Event Viewer).  
   - *Tip:* Think of it as a “What happened?” list with ID tags for easy tracking.  

2. **Linux Workstation**  
   - Logs: Stored in places like `/var/log/httpd` (web stuff), `/var/log/cron` (scheduled tasks), `/var/log/auth.log` (logins).  
   - Example: “May 28 - cron job started!”  
   - *Tip:* Picture it as folders full of notes about the system’s day.

3. **Web Server**  
   - Logs: Requests like “Someone visited /cgi-bin/try/” (in `/var/log/apache`).  
   - *Tip:* Imagine it as a guestbook for web visitors.

**How SIEM Gets Logs (Ingestion):**  
- **Agent/Forwarder:** A tiny tool on devices sends logs to SIEM.  
- **Syslog:** A common way to ship logs from servers to SIEM fast.  
- **Manual Upload:** Add old logs by hand (like in Splunk).  
- **Port-Forwarding:** Devices send logs to a specific SIEM “door” (port).  

**Why It’s Cool:** Logs help spot trouble (like attacks) by showing what’s normal or weird.

**Remembering Trick:** Think of SIEM as a librarian collecting daily “storybooks” (logs) from devices to read for clues!

---


### Why SIEM

**Main Idea:** SIEM watches network logs, connects the dots, and warns you about threats so you can act fast.

**Why It’s Awesome:**  
- Links events (like a login + weird file access) to spot trouble.  
- Shows what’s happening on devices (host) and between them (network).  
- Helps analysts catch new threats and respond quickly.  
- Hunts sneaky problems rules might miss.  

**SIEM in Action:**  
- Part of a Security Operations Center (SOC).  
- Checks logs, flags issues (like “Too many failed logins!”), and alerts analysts.

**SOC Analysts Use SIEM To:**  
- Watch and dig into alerts.  
- Sort real threats from false alarms.  
- Fix noisy rules.  
- Report stuff and fill visibility gaps.

**Remembering Trick:** Think of SIEM as a detective linking clues from a network’s “diary” to catch bad guys!

---


### Analyzing Logs & Alerts

**Main Idea:** SIEM grabs logs, checks them with rules, and alerts analysts to investigate weird stuff.

**How It Works:**  
- Logs come in (via agents, ports, etc.) and SIEM scans for bad patterns using rules.  
- If a rule “trips” (condition met), an alert pops up for analysts to check.

**Dashboards:**  
- SIEM’s “control room” shows summaries like:  
  - Alerts, failed logins, top websites, rule triggers.  
- Default ones exist, but you can make your own.  
- *Tip:* Think of it as a network’s “highlight reel.”

**Correlation Rules:**  
- Rules are like “if this, then alert!” Examples:  
  - 5 failed logins in 10 seconds? Alert!  
  - USB plugged in (if banned)? Alert!  
  - Big data leaving (25 MB+)? Alert!  
- *Example Rule:* If Event ID 104 (log cleared) hits, yell “Event Log Cleared!”  
- *Another:* If “whoami” runs (Event ID 4688), shout “WHOAMI Detected!”

**Investigating Alerts:**  
- Analysts watch dashboards, see alerts, and dig in.  
- Steps:  
  - False? Tweak the rule.  
  - True? Investigate more—talk to people, isolate devices, block IPs.

**Remembering Trick:** Picture SIEM as a security guard watching camera feeds (logs), ringing a bell (alert) when something’s off!
