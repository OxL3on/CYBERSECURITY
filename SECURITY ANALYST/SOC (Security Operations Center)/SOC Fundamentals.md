# SOC Fundamentals:

### Introduction to SOC

**Main Topic:**  
A **SOC (Security Operations Center)** is a dedicated team that works 24/7 to monitor an organization’s network and systems to protect against cyber threats.

**Key Points:**  
1. **Why SOC is Needed:**  
   - Technology makes life easier but also increases risks.  
   - Sensitive data (secrets) is now stored digitally, not in physical files.  
   - Cyber threats are growing daily, and traditional security isn’t enough.  

2. **What SOC Does:**  
   - Monitors networks and systems for suspicious activity.  
   - Prevents damage from cyberattacks by acting quickly.  

3. **How It Works:**  
   - The SOC team works non-stop (24/7).  
   - They detect and respond to threats in real-time.  

**-----**  
Imagine your organization’s network is like a house with many doors and windows. A SOC is like a security guard who watches all entrances 24/7, ready to stop anyone trying to break in. Without this guard, intruders could sneak in, steal valuables, or cause chaos.

**Remembering Tip:**  
Think of SOC as the "always-on" protector for your digital assets. If there’s a breach, they’re the first to know and act!  

---
---


### Purpose and Components of SOC

**Main Topic:**  
The SOC team focuses on **Detecting** and **Responding** to security incidents using the three pillars: **People, Process, and Technology**.


### **Key Points:**

#### **1. Detection**
- **Detect Vulnerabilities:**  
  - Weaknesses in software (e.g., unpatched Windows computers) that attackers can exploit.  
  - Example: A SOC discovers a vulnerability in a server’s operating system.  

- **Detect Unauthorized Activity:**  
  - Spotting when someone uses stolen credentials (e.g., an employee’s username/password).  
  - Clues like unusual login locations help detect this.  

- **Detect Policy Violations:**  
  - Identifying actions against company rules, like downloading pirated files or sending sensitive data insecurely.  

- **Detect Intrusions:**  
  - Stopping unauthorized access, such as hackers exploiting web apps or infecting systems via malicious sites.  


#### **2. Response**
- Once an incident is detected, the SOC team responds by:  
  - Minimizing damage.  
  - Finding the root cause of the issue.  
  - Supporting the incident response team to fix the problem.  


#### **3. The Three Pillars of SOC**
- **People:** Skilled professionals who monitor and respond to threats.  
- **Process:** Proper procedures to handle incidents effectively.  
- **Technology:** Advanced tools to detect and respond to security issues.  

**-----**  
Think of a SOC like a fire station:  
- **People** are the firefighters.  
- **Process** is the plan for putting out fires.  
- **Technology** is the fire truck and equipment.  
Without all three working together, the fire can’t be controlled quickly or efficiently.


**Remembering Tip:**  
SOC = Detect + Respond, powered by **People, Process, and Technology**. These three pillars make the SOC strong and effective!  

---
---


### People in a SOC

**Main Topic:**  
The **SOC team** is made up of skilled individuals who play different roles to detect and respond to security threats effectively.


### **Key Points:**

1. **Why People Matter:**  
   - Even with advanced automation, humans are essential to filter out noise (false alarms) and focus on real threats.  
   - Example: A fire alarm going off due to cooking smoke vs. an actual fire—humans decide what’s truly harmful.  

2. **SOC Team Hierarchy and Roles:**  
   - **SOC Analyst (Level 1):**  
     - First responders to alerts.  
     - Perform basic checks to determine if a detection is harmful.  
     - Report findings through proper channels.  

   - **SOC Analyst (Level 2):**  
     - Investigate deeper into alerts flagged by Level 1.  
     - Correlate data from multiple sources for better analysis.  

   - **SOC Analyst (Level 3):**  
     - Experienced pros who proactively hunt for threats.  
     - Handle critical incidents, including containment, eradication, and recovery.  

   - **Security Engineer:**  
     - Deploy and configure security tools to ensure they work smoothly.  

   - **Detection Engineer:**  
     - Create rules/logic for security tools to detect harmful activities.  

   - **SOC Manager:**  
     - Oversees the SOC team and processes.  
     - Reports to the CISO (Chief Information Security Officer) on the organization’s security status.  


**-----**  
Think of the SOC team as a hospital emergency room:  
- **Level 1 Analysts** are like nurses triaging patients (basic checks).  
- **Level 2 Analysts** are doctors diagnosing complex cases.  
- **Level 3 Analysts** are specialists handling life-threatening conditions.  
- **Security Engineers** are the technicians maintaining medical equipment.  
- **Detection Engineers** write the protocols for identifying illnesses.  
- **SOC Manager** is the head doctor ensuring everything runs smoothly.  


**Remembering Tip:**  
The SOC team is like a sports team—each role has a specific job, but everyone works together to win (protect the organization).  

---
---



### Process in a SOC

**Main Topic:**  
The **SOC process** revolves around key activities like **Alert Triage**, **Reporting**, and **Incident Response/Forensics** to handle security threats effectively.


### **Key Points:**

1. **Alert Triage:**  
   - The first step in responding to alerts.  
   - Focuses on analyzing and prioritizing alerts based on severity.  
   - Answers the **5 Ws**:  
     - **What?** What happened? (e.g., Malware detected)  
     - **When?** When did it happen? (e.g., June 5, 2024, at 13:20)  
     - **Where?** Where was it detected? (e.g., Host: GEORGE PC)  
     - **Who?** Who is involved? (e.g., User: George)  
     - **Why?** Why did it happen? (e.g., Downloaded pirated software)  

2. **Reporting:**  
   - Harmful alerts are escalated as tickets to higher-level analysts.  
   - Reports include:  
     - All **5 Ws** answered.  
     - Detailed analysis with evidence (e.g., screenshots).  

3. **Incident Response and Forensics:**  
   - For critical alerts, high-level teams initiate **incident response**.  
   - **Forensics** involves analyzing system/network artifacts to find the root cause of an incident.  


**-----**  
Imagine a SOC team as detectives solving a crime:  
- **Alert Triage:** They get a call about a break-in (alert). First, they ask the **5 Ws**—What happened? When? Where? Who’s involved? Why did it happen?  
- **Reporting:** They document their findings and send the case file to senior detectives (higher-level analysts).  
- **Incident Response/Forensics:** If it’s a major crime, they dig deeper—collecting fingerprints, reviewing CCTV footage (forensics), and stopping further damage (incident response).  


**Remembering Tip:**  
Think of SOC processes like solving a mystery:  
- **Triage = Ask the 5 Ws.**  
- **Report = Share your findings.**  
- **Respond/Forensics = Dig deeper for the truth.**  

---
---



### Technology in a SOC

**Main Topic:**  
**Technology** refers to the security tools used in a SOC to detect and respond to threats efficiently, reducing manual effort.


### **Key Points:**

1. **Why Technology is Important:**  
   - Centralizes data from all devices and applications in the network.  
   - Automates detection and response, saving time and resources.  

2. **Key Security Solutions:**  
   - **SIEM (Security Information and Event Management):**  
     - Collects logs from devices (log sources) and uses rules to detect suspicious activity.  
     - Provides advanced features like user behavior analytics and threat intelligence using machine learning.  
     - **Focus:** Detection only.  

   - **EDR (Endpoint Detection and Response):**  
     - Monitors endpoints (e.g., computers, servers) in real-time and provides historical data.  
     - Allows detailed investigation and quick automated responses with a few clicks.  

   - **Firewall:**  
     - Acts as a barrier between internal and external networks (e.g., the Internet).  
     - Filters unauthorized traffic and blocks suspicious activity before it enters the network.  

3. **Other Tools:**  
   - Includes Antivirus, EPP, IDS/IPS, XDR, SOAR, etc.  
   - The choice of tools depends on the organization’s threat surface and resources.  


**Story/Example:**  
Think of a SOC’s technology as a home security system:  
- **SIEM** is like the central control panel that collects alerts from all sensors (cameras, door alarms) and tells you if something’s wrong.  
- **EDR** is like a smart camera that watches every room in detail and can lock doors automatically if it detects an intruder.  
- **Firewall** is like a fence around your house that keeps unwanted visitors out.  


**Remembering Tip:**  
SOC Technology = Tools that **detect**, **analyze**, and **respond** to threats automatically. Think of them as your digital "security guards"!  
