### Wireshark

#### **What is Wireshark?**
Wireshark is a powerful tool for analyzing network traffic. It's not an Intrusion Detection System (IDS), meaning it doesn't alert you to threats but helps you inspect network packets in detail. You need strong investigative skills to spot issues or anomalies.


### **Uses of Wireshark**
1. **Troubleshooting Networks**  
   Identify issues like network congestion or failures.
2. **Detecting Security Anomalies**  
   Find rogue devices, unusual port activity, or suspicious traffic.
3. **Learning Protocols**  
   Understand how protocols work by analyzing response codes and payloads.


### **Wireshark Interface Overview**
Wireshark's interface consists of the following sections:
1. **Toolbar**  
   Quick access to features like filters, sorting, and exporting data.
2. **Display Filter Bar**  
   The main area for filtering traffic data.
3. **Recent Files**  
   A list of previously opened packet capture (PCAP) files.
4. **Capture Filter & Interfaces**  
   Choose where to capture traffic (e.g., `eth0`, `lo`).
5. **Status Bar**  
   Shows current settings, selected interface, and packet counts.


### **Loading PCAP Files**
- Open a PCAP file via:
  - File menu.
  - Drag-and-drop.
  - Double-clicking the file.
- Wireshark displays packets in **three panes**:
  1. **Packet List Pane**  
     Overview of packets with source, destination, protocol, etc.
  2. **Packet Details Pane**  
     In-depth breakdown of the selected packet's protocols.
  3. **Packet Bytes Pane**  
     Hexadecimal and ASCII data for the selected packet.


### **Color-Coding Packets**
- Packets are color-coded by protocol and other conditions for quick analysis.
- Two types of rules:
  - **Temporary Rules**: Active only during the session.
  - **Permanent Rules**: Saved and used across sessions.
- Customize colors via:
  - **View > Coloring Rules** for permanent rules.
  - **View > Conversation Filter** for temporary rules.


### **Traffic Sniffing**
- Use these buttons:
  - **Blue Shark Button**: Start capturing traffic.
  - **Red Button**: Stop capturing.
  - **Green Button**: Restart sniffing.
- The status bar shows the selected interface and captured packet count.


### **Merging PCAP Files**
- Combine multiple PCAP files:
  1. Go to **File > Merge**.
  2. Select the file to merge.
  3. Save the newly created file.


### **Viewing File Details**
- Find file information (hashes, capture time, comments, etc.):
  - Go to **Statistics > Capture File Properties**.
  - Click the PCAP icon in the bottom-left corner.


### **Key Notes**
- **Wireshark is a passive tool**: It reads packets but doesn’t modify them.
- Effective use depends on your ability to interpret data.  
- Explore features like filters, color rules, and file merging to maximize efficiency.

---
---


### **Wireshark: Packet Dissection**

#### **What is Packet Dissection?**
Packet dissection (or protocol dissection) is the process of breaking down a packet to analyze its details, using the OSI model's layers as a framework. Wireshark supports many protocols for this and even allows custom dissection scripts.


### **Using Packet Dissection in Wireshark**
- **How it works:**  
  - Click on a packet in the **Packet List Pane** to see its details in the **Packet Details Pane**.  
  - The highlighted section in the **Packet Details Pane** corresponds to the data shown in the **Packet Bytes Pane**.
  - Double-clicking opens the details in a new window.


### **Breaking Down a Packet (Based on OSI Layers)**  
Wireshark divides packets into distinct layers, showing details from Physical to Application layers.

1. **Frame (Layer 1)**:  
   - Physical layer information about the packet or frame.  

2. **Source [MAC] (Layer 2)**:  
   - Source and destination MAC addresses from the Data Link layer.  

3. **Source [IP] (Layer 3)**:  
   - Source and destination IPv4 addresses from the Network layer.

4. **Protocol (Layer 4)**:  
   - Protocol details (e.g., TCP/UDP) and source/destination ports from the Transport layer.

5. **Protocol Errors**:  
   - Extra details about TCP segments needing reassembly.

6. **Application Protocol (Layer 5)**:  
   - Information about the specific protocol used (e.g., HTTP, FTP, or SMB) from the Application layer.

7. **Application Data**:  
   - Protocol-specific data being carried by the application.


### **Example: Dissecting an HTTP Packet**
Imagine analyzing an HTTP request in Wireshark:  
- Layer 1 shows the packet frame.  
- Layer 2 displays MAC addresses for the devices involved.  
- Layer 3 lists the source and destination IPs.  
- Layer 4 reveals that the packet uses TCP, with specific port numbers.  
- Layer 5 provides the HTTP request details.  
- Application Data (part of Layer 5) shows the actual content of the HTTP request.


### **Why is this Useful?**
- Each layer gives critical information for troubleshooting and investigating network behavior.
- By following the OSI layers, you can isolate and analyze specific issues, such as protocol errors or unusual traffic.

---
---


