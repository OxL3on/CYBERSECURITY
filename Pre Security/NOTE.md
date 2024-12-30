### **Offensive security intro**  
#### **Core Concept**  
- **"Think like a hacker to outsmart one":** The essence of offensive security is understanding and anticipating hacker tactics.  

#### **What is Offensive Security?**  
- Breaking into computer systems.  
- Exploiting software bugs.  
- Finding loopholes in applications.  
- Gaining unauthorized access (in a controlled, legal context).  

#### **Goal**  
- Understand how hackers operate.  
- Use this knowledge to strengthen system defenses.  

#### **Learning Journey**  
- **Hands-on Practice:**  
  - Guided exploration of hacking techniques.  
  - Legal and safe environments (ex. TryHackMe room).  
- **Outcome:**  
  - Understand the operation of ethical hackers.  
  - Learn to identify and patch vulnerabilities in systems.

---
---

### Defensive Security Intro  

**Definition**  
Defensive security focuses on:  
1. **Preventing intrusions**: Stopping attacks before they happen.  
2. **Detecting and responding to intrusions**: Identifying attacks and taking proper action.  

**Blue Teams**  
Blue teams are integral to defensive security, tasked with protecting systems, networks, and data.  


**Tasks in Defensive Security**  

1. **User Cybersecurity Awareness**  
   - Train users to recognize and respond to cyber threats.  
   - Prevent attacks targeting user systems (e.g., phishing).

2. **Documenting and Managing Assets**  
   - Keep an inventory of all systems and devices.  
   - Identify what needs to be secured.

3. **Updating and Patching Systems**  
   - Apply updates and patches to address known vulnerabilities.  
   - Ensure systems, servers, and network devices are up-to-date.  

4. **Setting Up Preventative Security Devices**  
   - **Firewalls**:  
     - Control network traffic (inbound and outbound).  
   - **Intrusion Prevention Systems (IPS)**:  
     - Detect and block traffic matching known attack patterns.

5. **Setting Up Logging and Monitoring Devices**  
   - Monitor network activity to identify suspicious behavior.  
   - Detect unauthorized devices or malicious actions in the network.  

#### **1. Security Operations Center (SOC)**
- **Purpose and Role**: Understand the responsibilities of a SOC in monitoring and detecting cybersecurity events.
- **Key Focus Areas**:
  - Handling vulnerabilities and applying patches.
  - Detecting and managing policy violations.
  - Identifying unauthorized activity.
  - Detecting and responding to network intrusions.

#### **2. Threat Intelligence**
- **Definition and Purpose**:
  - Gathering and analyzing information about adversaries.
  - Understanding their tactics, techniques, and procedures (TTPs).
  - Preparing a threat-informed defense.
- **Process**:
  - Collecting data (local and public sources).
  - Processing and analyzing data to understand attackers’ motives.
  - Developing actionable recommendations.

#### **3. Digital Forensics and Incident Response (DFIR)**

##### **Digital Forensics**
- **Areas of Focus**:
  - Analyzing file systems for deleted or overwritten data.
  - Examining system memory to detect in-memory attacks.
  - Investigating system logs and network logs to gather evidence.
- **Applications**:
  - Investigating intellectual property theft and cyber espionage.
  - Tracing attack origins and gathering evidence for prosecution.

##### **Incident Response**
- **Phases**:
  1. **Preparation**: Establishing trained teams and preventative measures.
  2. **Detection and Analysis**: Identifying and assessing the severity of incidents.
  3. **Containment, Eradication, and Recovery**:
     - Stopping the spread of the attack.
     - Removing malicious elements.
     - Restoring systems to operational status.
  4. **Post-Incident Activity**: Reporting and learning from the incident.
- **Goal**: Minimize damage and recover quickly.

#### **4. Malware Analysis**
- **Types of Malware**:
  - **Viruses**: Self-replicating code that alters or deletes files.
  - **Trojan Horses**: Disguised programs that carry hidden malicious functionality.
  - **Ransomware**: Encrypts files and demands payment for decryption.
- **Analysis Techniques**:
  - **Static Analysis**: Examining malware without executing it.
  - **Dynamic Analysis**: Observing malware behavior in a controlled environment.


---
---

### Cybersecurity Careers Overview

Cybersecurity careers are in high demand, offering high salaries, exciting work, and job security. There are over 3.5 million unfilled cybersecurity positions globally, with roles ranging from offensive pentesting to defensive security.



### **Why Choose a Career in Cybersecurity**
1. **High Pay**: Competitive starting salaries.
2. **Exciting Work**: Engage in legally hacking systems or defending against cyberattacks.
3. **Demand**: Significant skill shortage ensures job stability and opportunities.



### **Key Roles and Responsibilities**

#### **1. Security Analyst**
- **Role**: Analyze and monitor security across organizations to prevent attacks.
- **Responsibilities**:
  - Work with stakeholders to analyze cybersecurity needs.
  - Compile reports on network security, documenting issues and measures.
  - Develop security plans using research on attack tools and trends.



#### **2. Security Engineer**
- **Role**: Develop and implement solutions to counter vulnerabilities and attacks.
- **Responsibilities**:
  - Test and screen security measures in software.
  - Monitor and update networks to mitigate risks.
  - Identify and deploy necessary security systems.



#### **3. Incident Responder**
- **Role**: Respond efficiently to breaches and cyber incidents in real-time.
- **Responsibilities**:
  - Develop actionable incident response plans.
  - Maintain best practices for security and support incident measures.
  - Produce post-incident reports and adapt strategies for future threats.
- **Metrics to Monitor**:
  - **MTTD**: Mean Time to Detect.
  - **MTTA**: Mean Time to Acknowledge.
  - **MTTR**: Mean Time to Recover.



#### **4. Malware Analyst**
- **Role**: Analyze malicious programs to understand their behavior and detect threats.
- **Responsibilities**:
  - Perform static analysis (reverse engineering) of malware.
  - Conduct dynamic analysis by observing malware in controlled environments.
  - Document findings and create detection methods.
- **Skills**:
  - Strong programming knowledge, especially in Assembly and C.



#### **5. Penetration Tester**
- **Role**: Test the security of systems by simulating hacking attempts.
- **Responsibilities**:
  - Test computer systems, networks, and applications.
  - Perform security assessments and audits.
  - Report vulnerabilities and recommend preventive measures.


#### **6. Red Teamer**
- **Role**: Simulate real-world attacks to test detection and response capabilities.
- **Responsibilities**:
  - Imitate threat actor behavior to uncover vulnerabilities.
  - Evaluate detection, response, and threat intelligence procedures.
  - Provide actionable insights to improve defense mechanisms.

---
---

### Networking Essentials in Cybersecurity

#### **What is a Network?**
- A network is a connection between two or more devices to exchange information or resources.
- Examples of non-technical networks: 
  - Public transportation systems.
  - National power grids.
  - Postal systems.
- **In Computing**: Networks connect devices like laptops, phones, security cameras, traffic lights, etc., enabling communication and data sharing.


#### **Types of Networks**
1. **Private Network**: Connects devices within a confined space, e.g., home or office networks.
2. **Public Network**: Connects multiple private networks to form a larger network, e.g., the Internet.

#### **The Internet**
- A massive public network made up of smaller private networks.
- Origin: Started as ARPANET in the 1960s; evolved into the Internet in 1989 with Tim Berners-Lee's World Wide Web.


### **Device Identification on Networks**
Devices must be identifiable, similar to humans having:
- **Names** (can change) → **IP Address** (temporary and can be reassigned).
- **Fingerprints** (permanent) → **MAC Address** (unique hardware identifier).

#### **IP Address**
- **Definition**: A numerical label that identifies a device on a network.
- **Types**:
  - **Private IP**: Identifies devices within a private network.
  - **Public IP**: Identifies a device on the Internet, provided by ISPs.
- **Versions**:
  - **IPv4**: Supports ~4.29 billion addresses (shortage of available addresses).
  - **IPv6**: Supports 2¹²⁸ addresses (~340 trillion trillion trillion), solving IPv4 shortages.

#### **MAC Address**
- **Definition**: A 12-character hexadecimal address assigned to a device's network interface by the manufacturer.
- **Structure**:
  - First six characters: Manufacturer identifier.
  - Last six characters: Unique device identifier.
- **Spoofing**: MAC addresses can be faked, bypassing poorly designed security measures.


### **Key Networking Tools**
#### **Ping**
- **Function**: Checks connection reliability between devices using ICMP (Internet Control Message Protocol).
- **How it Works**:
  - Sends an **ICMP echo request** to a target device.
  - Receives an **ICMP echo reply** to measure connection performance (e.g., latency).
- **Usage**: `ping <IP address>` or `ping <website URL>`.


### **Important Concepts**
1. **Protocols**: Rules that ensure devices communicate in the same "language" across networks.
2. **IP Addressing & Subnetting**: Techniques to organize and manage IP addresses.
3. **Network Integration**: Networks support crucial services like data collection, electricity delivery, and traffic management.

---
---

### Notes on LAN Topologies, Switches, Routers, Subnetting, ARP, and DHCP

#### **1. LAN Topologies**
- **Star Topology**:
  - Devices connect to a central switch/hub.
  - **Advantages**: Scalable, reliable.
  - **Disadvantages**: Expensive; central device failure disrupts the network.

- **Bus Topology**:
  - Devices share a single backbone cable.
  - **Advantages**: Cost-efficient, easy to set up.
  - **Disadvantages**: Prone to bottlenecks, difficult troubleshooting, single point of failure.

- **Ring Topology**:
  - Devices connected in a loop, forwarding data in one direction.
  - **Advantages**: Minimal bottlenecks, easy troubleshooting.
  - **Disadvantages**: Inefficient data travel, complete network failure if one device/cable breaks.

#### **2. Switches**
- Connect multiple devices via ports (e.g., 4, 8, 16, 24, etc.).
- Efficiently send data only to intended devices (unlike hubs).
- Can connect to routers for increased redundancy (multiple data paths).

#### **3. Routers**
- Connect networks and facilitate data routing.
- Use **routing tables** to find paths for data transfer.
- Essential for connecting to external networks (e.g., the Internet).

#### **4. Subnetting**
- **Definition**: Divides a large network into smaller, manageable subnetworks.
- Benefits:
  - **Efficiency**: Reduces congestion by segmenting networks.
  - **Security**: Isolates sensitive devices (e.g., staff vs. public networks in a café).
  - **Control**: Assign specific resources to specific network segments.
- **Components of Subnetting**:
  - **Network Address**: Identifies the network (e.g., `192.168.1.0`).
  - **Host Address**: Identifies individual devices (e.g., `192.168.1.100`).
  - **Default Gateway**: Device facilitating communication outside the subnet (e.g., `192.168.1.254`).

#### **5. Address Resolution Protocol (ARP)**
- **Purpose**: Maps IP addresses to MAC addresses.
- **How it works**:
  - Devices maintain an ARP cache (ledger of IP-MAC mappings).
  - Sends **ARP Request**: "Who owns this IP?"
  - Receives **ARP Reply**: Response with the MAC address.
- ARP is essential for intra-network device communication.

#### **6. Dynamic Host Configuration Protocol (DHCP)**
- Automates IP address assignment to devices on a network.
- DHCP Process:
  1. **DHCP Discover**: Device requests IP from the server.
  2. **DHCP Offer**: Server offers an available IP.
  3. **DHCP Request**: Device confirms acceptance of the IP.
  4. **DHCP ACK**: Server confirms the assignment.

### Key Takeaways:
1. **Topology Selection**: Each topology has distinct use cases; star topology is most common for reliability.
2. **Switches and Routers**: Essential for efficient data flow and connectivity in larger networks.
3. **Subnetting**: Provides better control, security, and efficiency in complex networks.
4. **ARP and DHCP**: Critical protocols ensuring proper identification and connectivity within networks.






## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
