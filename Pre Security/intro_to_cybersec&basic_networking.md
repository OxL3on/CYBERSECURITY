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

---
---

### OSI Model - Key Points

The OSI (Open Systems Interconnection) Model is a fundamental framework in networking that defines how devices communicate and interpret data. It consists of **seven layers**, each with specific responsibilities:

#### **Layer 1: Physical Layer**  
- Focuses on physical hardware and data transmission (binary signals: 0s and 1s).  
- Includes cables, switches, and network interface cards (NICs).  

#### **Layer 2: Data Link Layer**  
- Handles **MAC addressing** and physical addressing.  
- Adds the MAC address of the destination device for accurate delivery.  
- NICs provide unique MAC addresses (hardware-burned).  
- Responsible for data formatting for physical transmission.

#### **Layer 3: Network Layer**  
- Performs **routing** and reassembly of data packets.  
- Determines the **optimal path** based on factors like speed, reliability, and the number of hops.  
- Uses **IP addressing** for device identification.  
- Routers operate at this layer (Layer 3 devices).

#### **Layer 4: Transport Layer**  
- Responsible for **data transmission protocols**:  
  - **TCP (Transmission Control Protocol):** Reliable and accurate, uses error checking, slower but ensures data integrity (e.g., file sharing, email).  
  - **UDP (User Datagram Protocol):** Faster but less reliable, used for streaming, device discovery, etc.  

**TCP Advantages:**  
- Guarantees accuracy.  
- Synchronizes devices to prevent flooding.  

**TCP Disadvantages:**  
- Requires a stable connection.  
- Slower due to reliability features.  

**UDP Advantages:**  
- Faster and flexible for developers.  
- No reserved connection, better for unstable connections.  

**UDP Disadvantages:**  
- No guarantee of data delivery.  
- Unstable connections lead to lost data.  

#### **Layer 5: Session Layer**  
- Manages **session creation, maintenance, and termination**.  
- Ensures a unique session for data exchange.  
- Provides "checkpoints" to resend only recent data if lost.  

#### **Layer 6: Presentation Layer**  
- Acts as a **translator** for data, ensuring uniformity across different systems.  
- Handles **data encryption** (e.g., HTTPS for secure sites).  

#### **Layer 7: Application Layer**  
- Closest to the user. Defines protocols for how applications interact with data.  
- Includes familiar services like email (SMTP), web browsing (HTTP/HTTPS), file sharing, and DNS.

### Additional Concepts

- **Encapsulation:** Process of adding information at each layer as data is transmitted.  
- **Protocols:**  
  - Layer 4: TCP, UDP.  
  - Layer 7: DNS, HTTP, HTTPS, SMTP.
 
---
---

**Networking Fundamentals: Packets, Frames, TCP, and UDP**

### **Packets and Frames**
- **Frames (Layer 2):** Data at the Data Link Layer; no IP addresses. Encapsulation wraps packets inside frames for transmission.
- **Packets (Layer 3):** Include IP addresses for routing; small data units that ensure efficient communication.

**Encapsulation:** Wrapping data with headers and trailers as it moves down the OSI or TCP/IP layers.

**Packet Structure:**
- **Time to Live (TTL):** Prevents packets from endlessly circulating.
- **Checksum:** Ensures data integrity.
- **Source/Destination IP:** Defines the sender/receiver's IP.
- **Source/Destination Port:** Indicates the sender's random port and the receiver's service port.

### **TCP (Transmission Control Protocol)**
- **Connection-oriented:** Ensures reliable communication with error checking.
- **Three-way Handshake:**
  1. **SYN:** Client initiates synchronization.
  2. **SYN/ACK:** Server acknowledges and synchronizes.
  3. **ACK:** Client confirms synchronization.
- **Sequence Numbers:** Ensure data is reconstructed in the correct order.
- **TCP Closing:**
  - Devices exchange **FIN** and **ACK** messages to close connections properly.

**TCP Headers:**
- **Sequence/Acknowledgment Numbers:** For tracking data packets.
- **Checksum:** Validates data integrity.
- **Flags (e.g., SYN, ACK, FIN):** Manage connection states.

**Advantages of TCP:**
- Guarantees data delivery and order.
- Synchronizes devices to prevent flooding.

**Disadvantages of TCP:**
- Slower than UDP due to reliability processes.
- Requires a stable connection.

### **UDP (User Datagram Protocol)**
- **Connectionless:** No handshake or acknowledgment; stateless protocol.
- **Usage Scenarios:** Suitable for non-critical data like video streaming or voice chats.
- **Faster but less reliable** than TCP.

**UDP Headers:**
- **Time to Live (TTL):** Expiration timer for packets.
- **Source/Destination Address:** Identifies sender and receiver IPs.
- **Source/Destination Port:** Indicates sender's random port and receiver's service port.

**Advantages of UDP:**
- Faster due to minimal overhead.
- Flexible for applications to manage data flow.

**Disadvantages of UDP:**
- No guarantees for data delivery or integrity.
- Poor user experience with unstable connections.

### **Comparison of TCP and UDP**
| **Feature**               | **TCP**                        | **UDP**                    |
|---------------------------|--------------------------------|---------------------------|
| **Reliability**            | Ensures data integrity         | No guarantee of delivery  |
| **Speed**                  | Slower due to overhead         | Faster, minimal overhead  |
| **Use Cases**              | File sharing, email, browsing  | Streaming, voice chats    |
| **Connection Type**        | Connection-oriented            | Connectionless            |

**Key Takeaway:**  
- Use TCP for accuracy-critical tasks (e.g., email, file transfer).  
- Use UDP for speed-critical tasks where some data loss is acceptable (e.g., video streaming).


---
---

### Networking Essentials  

#### **1. Port Forwarding**  
- **Purpose**: Allows public access to internal network services (e.g., web servers).  
- **Setup**: Configured at the router level.  
- **Relation to Firewalls**: Opens specific ports, while firewalls control traffic through those ports.  

#### **2. Firewalls**  
- **Purpose**: Filters traffic entering and leaving a network.  
- **Key Rules**:
  - Traffic source and destination.
  - Destination port (e.g., port 80 for HTTP).
  - Protocol type (TCP/UDP).  
- **Types**:
  - **Stateful**: Examines entire connections, dynamic but resource-heavy.  
  - **Stateless**: Examines individual packets, faster but rule-dependent.  

#### **3. VPNs (Virtual Private Networks)**  
- **Purpose**: Securely connect separate networks over the Internet.  
- **Benefits**:
  - Connects networks across locations.  
  - Ensures privacy through encryption.  
  - Provides anonymity for sensitive activities.  
- **Common VPN Technologies**:
  - **PPP**: For authentication and encryption.  
  - **PPTP**: Easy to set up, weaker encryption.  
  - **IPSec**: Strong encryption, harder to configure.  
- **Ethical Hacking Application**: Protects identity when interacting with vulnerable machines.  

---

#### **4. Routers**  
- **Role**: Connect networks and determine data paths (Layer 3).  
- **Routing Decisions**:
  - Shortest path.
  - Most reliable path.
  - Fastest medium (e.g., copper vs. fiber).  
- **Capabilities**: Includes port forwarding and firewall configurations.  

#### **5. Switches**  
- **Purpose**: Connect multiple devices within a network.  
- **Types**:
  - **Layer 2 Switch**:
    - Operates using MAC addresses.  
    - Forwards data (frames) without understanding IP protocols.  
  - **Layer 3 Switch**:
    - Handles both frame forwarding and packet routing.  
    - Supports **VLANs** for network segmentation.  
- **VLAN Example**: Enables departments to share Internet access but restrict inter-communication for security.  

#### **Critical Applications in Ethical Hacking**  
1. **Port Scanning**: Understand open ports and services via port forwarding.  
2. **Firewall Testing**: Identify misconfigurations or rules to bypass.  
3. **VPN Usage**: Mask identity and safely interact with target systems.  
4. **Routing Knowledge**: Exploit weak routing configurations or sniff traffic.  
5. **Switch Operations**: Leverage VLAN misconfigurations for lateral movement.  




## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
