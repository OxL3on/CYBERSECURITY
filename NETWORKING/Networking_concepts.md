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


