### DHCP (Dynamic Host Configuration Protocol)

#### **What is DHCP?**
- DHCP is an **application-level protocol** used to automatically assign network configurations to devices on a network.  
- **Primary purpose:** Eliminate the need for manual IP configuration and prevent IP address conflicts.  
- Operates using **UDP**:  
  - Server listens on **port 67**.  
  - Client communicates via **port 68**.  

#### **Essential Network Configuration Provided by DHCP**
1. **IP address** (with subnet mask).  
2. **Gateway (router):** Routes packets outside the local network.  
3. **DNS server:** Resolves domain names into IP addresses.

#### **DHCP Process: The DORA Steps**
The **DORA** process involves four key steps:  
1. **DHCP Discover:**  
   - The client broadcasts a `DHCPDISCOVER` message to locate a DHCP server.  
   - Broadcast sent from `0.0.0.0` to `255.255.255.255` since the client has no IP yet.  

2. **DHCP Offer:**  
   - The server responds with a `DHCPOFFER` message containing:  
     - An available IP address.  
     - Network configuration details (e.g., subnet mask, gateway, DNS server).  

3. **DHCP Request:**  
   - The client replies with a `DHCPREQUEST` message to indicate it accepts the offered IP address.  

4. **DHCP Acknowledge (ACK):**  
   - The server confirms with a `DHCPACK` message, finalizing the assignment.  
   - The client can now use the assigned IP and configuration.  

#### **Example Packet Exchange (Captured with Wireshark):**

```plaintext
1   0.000000      0.0.0.0 → 255.255.255.255 DHCP 342 DHCP Discover - Transaction ID 0xfb92d53f
2   0.013904 192.168.66.1 → 192.168.66.133 DHCP 376 DHCP Offer    - Transaction ID 0xfb92d53f
3   4.115318      0.0.0.0 → 255.255.255.255 DHCP 342 DHCP Request  - Transaction ID 0xfb92d53f
4   4.228117 192.168.66.1 → 192.168.66.133 DHCP 376 DHCP ACK      - Transaction ID 0xfb92d53f
```

#### **Key Observations in the Packet Exchange**
- **Client starts without an IP:**  
  - Uses `0.0.0.0` as the source IP and `255.255.255.255` (broadcast) as the destination.  
  - Relies on its **MAC address** for identification.  

- **Broadcast MAC address:**  
  - `ff:ff:ff:ff:ff:ff` used for initial communication before IP is assigned.  

- **Server offers configuration:**  
  - Sends the `DHCPOFFER` to the client’s MAC address using the proposed IP.  

- **Assigned IP:**  
  - Client receives a **leased IP address**, gateway, and DNS server details.  

#### **Advantages of DHCP**
1. **Automation:** Simplifies network configuration, especially for mobile devices.  
2. **Prevents conflicts:** Ensures unique IP assignments within a network.  
3. **Scalability:** Efficiently manages large networks without manual intervention.

#### **Limitations and Security Concerns**
1. **IP spoofing:** Malicious devices could mimic a DHCP server.  
2. **Lack of encryption:** Communication is unprotected, posing a risk in untrusted environments.  
3. **Static IPs for servers:** DHCP is not ideal for devices requiring fixed IP addresses.

#### **Summary**
DHCP automates the process of assigning essential network settings, ensuring seamless connectivity for devices. By following the **DORA** process, it dynamically configures IP addresses, reducing manual effort and preventing conflicts. However, security measures (e.g., trusted DHCP servers) are crucial in sensitive environments.


---
---


