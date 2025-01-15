### OSI Model

The **OSI (Open Systems Interconnection) model** is a theoretical framework for understanding network communication, developed by the International Organization for Standardization (ISO). It consists of **7 layers**, each with a specific role. Here's a concise breakdown of the layers with simple examples:  

#### **Layer 1: Physical Layer**
- **Purpose:** Handles physical connections and transmits raw binary data (0s and 1s).  
- **Examples:**  
  - Ethernet cables, optical fibers, WiFi signals (e.g., 2.4 GHz, 5 GHz).  
  - Devices like antennas and cables.  

#### **Layer 2: Data Link Layer**
- **Purpose:** Ensures reliable data transfer within the same network segment.  
- **Key Concepts:**  
  - **MAC Address:** Unique hardware address for devices (e.g., `00:1A:2B:3C:4D:5E`).  
  - Data transfer protocols: Ethernet (802.3), WiFi (802.11).  
- **Example:**  
  - A group of computers connected via a network switch in an office.  

#### **Layer 3: Network Layer**
- **Purpose:** Handles communication between different networks through routing and logical addressing.  
- **Key Concepts:**  
  - **IP Address:** Logical address for identifying devices on a network.  
  - Routing data through multiple paths.  
- **Examples:**  
  - Internet Protocol (IP), ICMP (ping), VPNs (IPSec).  

#### **Layer 4: Transport Layer**
- **Purpose:** Provides end-to-end communication and ensures reliable data delivery.  
- **Key Concepts:**  
  - Flow control, segmentation, error correction.  
- **Examples:**  
  - TCP (reliable communication), UDP (faster but less reliable).  

#### **Layer 5: Session Layer**
- **Purpose:** Manages sessions between applications, including starting, maintaining, and ending them.  
- **Example:**  
  - Remote Procedure Call (RPC), Network File System (NFS).  

#### **Layer 6: Presentation Layer**
- **Purpose:** Converts data into a readable format, handles encryption, compression, and encoding.  
- **Examples:**  
  - Encoding: ASCII, Unicode.  
  - File Formats: JPEG (images), MPEG (videos).  
  - Email attachments using MIME.  

#### **Layer 7: Application Layer**
- **Purpose:** Provides direct services to user applications.  
- **Examples:**  
  - HTTP (web browsing), FTP (file transfer), DNS (domain name lookup), SMTP (emails).  

### Quick Mnemonic to Remember the Layers:
"**Please Do Not Throw Spinach Pizza Away**" (Physical → Application, bottom to top).  

### Summary Table:
| **Layer Number** | **Layer Name**       | **Main Function**                        | **Examples**                     |
|-------------------|----------------------|------------------------------------------|-----------------------------------|
| 7                 | Application Layer    | Services for user applications           | HTTP, FTP, DNS, SMTP             |
| 6                 | Presentation Layer   | Data formatting, encryption, compression | Unicode, JPEG, MIME              |
| 5                 | Session Layer        | Session management                       | NFS, RPC                         |
| 4                 | Transport Layer      | End-to-end communication                 | TCP, UDP                         |
| 3                 | Network Layer        | Routing and logical addressing           | IP, ICMP, IPSec                  |
| 2                 | Data Link Layer      | Data transfer within a network segment   | Ethernet, WiFi                   |
| 1                 | Physical Layer       | Physical medium for data transmission    | Cables, WiFi signals             |

---
---


### TCP/IP Model

The **TCP/IP model** (Transmission Control Protocol/Internet Protocol) is a practical framework for network communication developed by the U.S. Department of Defense (DoD) in the 1970s. Its design ensures resilience, allowing networks to function even when parts are down, such as during a military attack.  


#### **Layers of the TCP/IP Model (4-Layer View):**  

1. **Application Layer**  
   - **What it does:** Handles user-facing services and combines OSI layers 5, 6, and 7 (Session, Presentation, Application).  
   - **Examples:**  
     - HTTP/HTTPS (web browsing), FTP (file transfer), SSH (remote access), SMTP/IMAP/POP3 (email).  

2. **Transport Layer**  
   - **What it does:** Manages end-to-end communication, reliability, and flow control (OSI layer 4).  
   - **Examples:**  
     - **TCP:** Reliable, connection-oriented (e.g., file downloads).  
     - **UDP:** Fast, connectionless (e.g., online gaming, video streaming).  

3. **Internet Layer**  
   - **What it does:** Handles routing and addressing across multiple networks (OSI layer 3).  
   - **Examples:**  
     - IP (Internet Protocol), ICMP (ping), IPSec (secure network connections).  

4. **Link Layer**  
   - **What it does:** Ensures communication between devices on the same network segment (OSI layers 1 & 2).  
   - **Examples:**  
     - Ethernet (802.3), WiFi (802.11).  


#### **5-Layer View:**  
Some textbooks, like *Computer Networking: A Top-Down Approach*, include a separate **Physical Layer** under the **Link Layer**, resulting in the following layers:  
- Application  
- Transport  
- Network  
- Link  
- Physical  

#### **Comparison with OSI Model:**  

| **OSI Model Layers**     | **TCP/IP Model Layers**    | **Examples**                       |
|---------------------------|----------------------------|-------------------------------------|
| Application (7)           | Application               | HTTP, FTP, SMTP, SSH               |
| Presentation (6)          |                           |                                     |
| Session (5)               |                           |                                     |
| Transport (4)             | Transport                 | TCP, UDP                           |
| Network (3)               | Internet                  | IP, ICMP, IPSec                    |
| Data Link (2)             | Link                     | Ethernet, WiFi                     |
| Physical (1)              |                           | Cables, signals                    |

---
---


### IP Addressing, Private Networks, and Routing

#### **IP Addresses Overview**
An **IP address** uniquely identifies a device on a network, much like a postal address identifies a home. The two main IP versions are:
- **IPv4:** Commonly represented as four octets (e.g., 192.168.0.1), with each octet ranging from 0 to 255. IPv4 uses 32 bits, allowing approximately \(2^{32}\) (4 billion) unique addresses.
- **IPv6:** Not covered here but provides a significantly larger address space.

#### **IPv4 Address Structure**
- **Octets:** Four groups of 8 bits (e.g., 192.168.66.89).
- **Network and Broadcast Addresses:**
  - **Network Address:** First address (e.g., 192.168.66.0).
  - **Broadcast Address:** Last address (e.g., 192.168.66.255).
- **Usable Addresses:** Range between these two addresses (e.g., 192.168.66.1 to 192.168.66.254).

#### **Subnetting**
- **Subnet Mask:** Defines the network portion of an IP address.
  - Example: `255.255.255.0` or `/24`.
  - `/24` means the first 24 bits are fixed, and the remaining 8 bits are for host addresses.
- **Subnet Range:** For `192.168.66.0/24`, usable addresses are `192.168.66.1–192.168.66.254`.

#### **Types of IP Addresses**
1. **Public IP Addresses:** Reachable from the internet (e.g., a web server’s IP).
2. **Private IP Addresses:** Reserved for internal networks and cannot directly access the internet.
   - Defined by **RFC 1918**:
     - `10.0.0.0 - 10.255.255.255` (`10/8`)
     - `172.16.0.0 - 172.31.255.255` (`172.16/12`)
     - `192.168.0.0 - 192.168.255.255` (`192.168/16`)

- **NAT (Network Address Translation):** A router translates private IPs to a public IP for internet access.

#### **Finding Your IP Address**
- **Windows Command:** `ipconfig`
- **Linux/UNIX Commands:**  
  - `ifconfig`
  - `ip a s` (or `ip address show`)

**Example Output (Linux):**
```
inet 192.168.66.89/24 brd 192.168.66.255
```
- `192.168.66.89/24`: Host IP with subnet mask `/24`.
- `192.168.66.255`: Broadcast address.


#### **Routing**
- A **router** functions like a postal office, directing packets to their destination.
- Operates at **Layer 3** (Network layer) and determines the best path for data packets.
- Data packets typically traverse multiple routers before reaching their final destination.


#### **Key Analogies**
1. **IP Address = Postal Address:** Enables unambiguous identification and communication.
2. **Router = Post Office:** Directs data to the next appropriate "network" or router for delivery.


#### **Tips for Memorization**
1. Memorize private IP ranges:
   - `10.0.0.0/8`
   - `172.16.0.0/12`
   - `192.168.0.0/16`
2. Practice identifying network, broadcast, and usable addresses in given subnets.

---
---


