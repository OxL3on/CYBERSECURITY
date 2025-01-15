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

---
---


### UDP and TCP


#### **Transport Protocols Overview**
Transport protocols enable processes on networked devices to communicate. The two primary protocols are:
- **UDP (User Datagram Protocol):** Connectionless and fast.
- **TCP (Transmission Control Protocol):** Connection-oriented and reliable.


#### **User Datagram Protocol (UDP)**
- **Layer:** Operates at Layer 4 (Transport Layer).
- **Connectionless:** No connection establishment is needed; data is sent directly to the target.
- **No Delivery Guarantee:** There is no confirmation or acknowledgment for packet delivery.
- **Use of Ports:**  
  - Identifies processes using **port numbers** (range: 1–65535; port 0 is reserved).
  - A port number is 16 bits (\(2^{16} - 1 = 65535\)).

**Analogy:**  
UDP is like standard mail service without delivery confirmation—cheaper and faster but unreliable.

**Use Cases:**  
- Streaming media
- Online gaming
- DNS lookups
- VoIP

#### **Transmission Control Protocol (TCP)**
- **Layer:** Operates at Layer 4 (Transport Layer).
- **Connection-Oriented:** Requires a connection to be established before data transfer.
- **Reliable Delivery:**
  - Sequence numbers ensure ordered data delivery.
  - Acknowledgment numbers confirm received data.
- **Three-Way Handshake:**  
  Establishes a connection using three steps:
  1. **SYN:** Client sends a packet with a **SYN** flag and its initial sequence number.
  2. **SYN-ACK:** Server responds with a packet containing both **SYN** and **ACK** flags, adding its own sequence number.
  3. **ACK:** Client sends a final acknowledgment (ACK) to confirm the handshake.

**Analogy:**  
TCP is like registered mail, where every step is acknowledged for reliability.

**Use Cases:**  
- Web browsing (HTTP/HTTPS)
- File transfer (FTP)
- Email (SMTP, IMAP, POP3)
- Remote login (SSH)


#### **Key Differences: UDP vs TCP**

| Feature                | UDP                        | TCP                         |
|------------------------|----------------------------|-----------------------------|
| **Connection Type**    | Connectionless             | Connection-oriented         |
| **Reliability**         | Unreliable                 | Reliable                    |
| **Speed**              | Faster (no overhead)       | Slower (due to overhead)    |
| **Delivery Guarantee** | No                        | Yes                         |
| **Use Cases**          | Streaming, DNS, Gaming     | Web, Email, File Transfer   |


#### **Ports in Both Protocols**
- A **port number** identifies the process communicating on the network.
- Ranges:
  - **Well-Known Ports (1–1023):** Reserved for standard services (e.g., HTTP - 80, HTTPS - 443).
  - **Registered Ports (1024–49151):** Assigned to user processes or applications.
  - **Dynamic/Ephemeral Ports (49152–65535):** Used temporarily for client connections.

---
---



### Encapsulation and the Life of a Packet

#### **Encapsulation**
Encapsulation is the process of adding headers (and sometimes trailers) at each layer of the OSI or TCP/IP model. This allows each layer to perform its specific function independently.  

**Key Steps:**
1. **Application Data:**  
   - The user inputs data (e.g., an email or search query).  
   - The application formats the data according to the application protocol.  
   - Data is passed to the transport layer.  

2. **Transport Protocol Segment or Datagram:**  
   - Transport layer (e.g., TCP or UDP) adds its header:  
     - **TCP Header:** Includes sequence numbers and acknowledgment for reliable delivery.  
     - **UDP Header:** Lightweight with source and destination ports for quick delivery.  
   - Creates a **TCP segment** or **UDP datagram** and sends it to the network layer.

3. **Network Packet:**  
   - Network layer (Internet layer) adds an **IP header**:
     - Includes source and destination IP addresses.
   - The resulting **IP packet** is sent to the link layer.  

4. **Data Link Frame:**  
   - Data link layer adds its own **header and trailer**:  
     - Includes physical addressing (e.g., MAC addresses).  
   - Creates an **Ethernet/WiFi frame** for physical transmission.  

The encapsulated frame is transmitted over the network. The process is reversed at the receiving end to extract the application data.


#### **Life of a Packet**
**Example Scenario:** Searching for a room on TryHackMe.  

1. **Application Layer:**  
   - You enter a search query and press enter.  
   - The browser creates an **HTTP request** using HTTPS and sends it to the transport layer.  

2. **Transport Layer:**  
   - **TCP connection:** Initiates a three-way handshake with the TryHackMe server.  
   - Adds the TCP header to create segments.  
   - Sends the segments to the Internet layer.

3. **Internet Layer (Network Layer):**  
   - Adds an **IP header**:  
     - Source IP: Your device.  
     - Destination IP: TryHackMe's server.  
   - Creates IP packets and passes them to the link layer.

4. **Data Link Layer:**  
   - Adds a **link layer header and trailer** for Ethernet or WiFi:  
     - Includes source and destination MAC addresses.  
   - Sends the frame to the router.

5. **Router Processing:**  
   - The router removes the link layer header and trailer.  
   - Inspects the destination IP address and forwards the packet along the appropriate path.  
   - Each router repeats this process until the packet reaches the destination network.  

6. **Destination Network:**  
   - The final router delivers the frame to the TryHackMe server.  
   - The server reverses the encapsulation process to extract the HTTP request.  

7. **Server Response:**  
   - The TryHackMe server processes the request, creates an HTTP response, and encapsulates it.  
   - The response packet travels back to your device, following the same steps in reverse.  

---
---



### Telnet

#### **What is Telnet?**
- **TELNET (Teletype Network):** A protocol for remote terminal connection that allows a user to interact with a remote system using text-based commands.  
- Operates on **TCP** and enables communication with any server listening on a specific **TCP port**.

#### **Key Features:**
- Simple text-based protocol.
- Initially used for remote administration but now considered insecure because data (including credentials) is transmitted in plain text.  
- Modern use is limited to testing and troubleshooting network services.


#### **Experimenting with Telnet**

1. **Starting Telnet:**
   - Command syntax:  
     ```bash
     telnet <MACHINE_IP> <PORT>
     ```

2. **Use Cases:**

   **a. Echo Server (Port 7):**  
   - The echo server repeats any text sent to it.  
   - Example Interaction:  
     ```bash
     telnet MACHINE_IP 7
     Trying MACHINE_IP...
     Connected to MACHINE_IP.
     Escape character is '^]'.
     Hello
     Hello
     ```
   - To close the connection, press `CTRL + ]` and type `quit`.

   **b. Daytime Server (Port 13):**  
   - The daytime server responds with the current date and time.  
   - Example Interaction:  
     ```bash
     telnet MACHINE_IP 13
     Trying MACHINE_IP...
     Connected to MACHINE_IP.
     Escape character is '^]'.
     Thu Jan 14 08:45:00 PM UTC 2025
     Connection closed by foreign host.
     ```

   **c. Web (HTTP) Server (Port 80):**  
   - Telnet can communicate with an HTTP server by sending HTTP requests.  
   - Example HTTP request to fetch the homepage:  
     ```bash
     telnet MACHINE_IP 80
     Trying MACHINE_IP...
     Connected to MACHINE_IP.
     Escape character is '^]'.
     GET / HTTP/1.1
     Host: telnet.thm
     
     HTTP/1.1 200 OK
     Content-Type: text/html
     [...]
     Connection closed by foreign host.
     ```
   - After typing the HTTP request, press **Enter twice** to send the request.


#### **Notes on Security Risks:**
- **Echo and Daytime Servers:**  
  - Considered insecure and should not be enabled on production systems.  
  - Can be exploited for reflection/amplification attacks.

- **Telnet Protocol:**  
  - Transmits data in plain text.  
  - Replaced by secure protocols like **SSH** for remote administration.


#### **Summary:**
Telnet is a simple but powerful tool for testing and debugging network services. Its primary modern usage includes:
- Verifying connectivity to specific ports.
- Testing services like HTTP, SMTP, or custom TCP-based protocols.
- **Recommendation:** Use **Telnet** for testing in controlled environments only, as it lacks encryption and is not suitable for secure communication.
