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


### Wireshark Packet Navigation

### **1. Packet Numbers**
- **Unique Numbering**: Each packet in a capture file is assigned a unique number, making it easy to locate specific events in large datasets.
- **Usage**: Use the **"Go" menu** or toolbar for quick navigation to a packet by number.


### **2. Finding Packets**
- **Search by Content**: Use the "Edit → Find Packet" menu to search packets by:
  - **Display Filter**: Apply predefined Wireshark filters.
  - **Hex**: Look for specific hexadecimal data.
  - **String**: Search for plain text (case-insensitive by default).
  - **Regex**: Use regular expressions for advanced matching.
- **Search Fields**: Ensure you search within the correct pane:
  - **Packet List**: Overview of packets.
  - **Packet Details**: Layer-specific breakdown.
  - **Packet Bytes**: Raw data in hex or ASCII format.


### **3. Marking and Commenting Packets**
- **Mark Packets**:
  - Use **"Edit → Mark Packet"** or right-click to flag packets of interest.
  - Marked packets appear in **black**.
  - Marks reset after closing the file.
- **Add Comments**:
  - Add notes to packets for collaborative or future analysis.
  - Comments are saved in the capture file and persist across sessions.


### **4. Exporting Packets and Objects**
- **Export Packets**: Share specific packets without including irrelevant data. Use the "File → Export Packet Dissections" menu.
- **Export Objects**: Extract files transferred over specific protocols like HTTP, SMB, or TFTP for further investigation.


### **5. Time Display Formats**
- Default format: "Seconds Since Beginning of Capture."
- Preferred format: UTC Time for better readability.
- Change via "View → Time Display Format."


### **6. Expert Info**
- **Purpose**: Highlights potential anomalies or errors.
- **Severity Levels**:
  - **Blue (Chat)**: Normal workflow information.
  - **Cyan (Note)**: Notable events like application errors.
  - **Yellow (Warn)**: Warnings, e.g., unusual codes.
  - **Red (Error)**: Critical issues like malformed packets.
- **Viewing**:
  - Status bar (lower-left corner).
  - "Analyze → Expert Information."


### **Examples for Better Understanding**
1. **Finding Intrusions**:
   - Search for "login failed" in string searches to identify brute force attempts.
2. **Marking Suspicious Packets**:
   - Flag packets with unusual protocols like `SMB` on an untrusted network.
3. **Exporting Malware**:
   - Extract a `.exe` file transferred over HTTP for malware analysis.

---
---


### **Wireshark Packet Filtering**

Wireshark provides two types of filtering mechanisms to refine captured data: **Capture Filters** and **Display Filters**. While capture filters determine what packets are saved during a live capture, display filters refine which packets are visible in the interface post-capture.


### **1. Display Filters**
- Used for investigating packets within a capture file.
- Filters can be applied by:
  - **Writing queries**: Directly entering filter expressions.
  - **Using the GUI**: Right-click on a field or value and select options like "Apply as Filter."

#### **Apply as Filter**
- The simplest way to filter traffic.
- Right-click on a field in the **Packet Details Pane** or use "Analyse → Apply as Filter."
- Wireshark generates and applies the filter automatically, showing only relevant packets in the **Packet List Pane.**
- The total number of packets (captured vs. displayed) is shown in the **status bar.**


### **2. Conversation Filters**
- Filters entire conversations (e.g., streams of packets between two IPs or ports).
- Ideal for analyzing interactions, not just single packets.
- Access via:
  - **Right-click menu** → "Conversation Filter."
  - **Analyse → Conversation Filter** menu.
- Hides unrelated packets, focusing on those linked to the chosen conversation.


### **3. Colourise Conversation**
- Highlights linked packets without hiding unrelated ones.
- Works with "Colouring Rules" to visually differentiate packets.
- Useful for quick identification of related traffic.
- Reset via "View → Colourise Conversation → Reset Colourisation."


### **4. Prepare as Filter**
- Generates a display filter query without applying it immediately.
- Query is editable in the **Display Filter Bar.**
- Allows combining filters using **logical operators** like "AND" and "OR."
- Useful for building complex filters.


### **5. Apply as Column**
- Adds specific fields/values as columns in the **Packet List Pane.**
- Helps track the occurrence of a value (e.g., IP address, port) across all packets.
- Columns can be enabled/disabled by clicking the column header.


### **6. Follow Stream**
- Reconstructs and displays raw application-level traffic for:
  - **TCP/UDP**: View continuous data streams.
  - **HTTP**: Rebuild request/response structures.
- Highlights:
  - **Blue**: Data from the server.
  - **Red**: Data from the client.
- Useful for:
  - Viewing unencrypted protocols.
  - Extracting data like usernames, passwords, or transmitted files.
- Access via:
  - **Right-click menu** → "Follow [Protocol] Stream."
  - **Analyse → Follow Stream.**
- To reset and view all packets, use the **"X button"** in the display filter bar.


### **Tips for Using Filters Effectively**
1. **Master Query Syntax**:
   - Example: `ip.src == 192.168.1.1` (Filter packets from source IP `192.168.1.1`).
   - Example: `tcp.port == 80` (Filter packets on TCP port 80).
2. **Combine Filters**:
   - Use `and`, `or`, and `not` for advanced filtering.
   - Example: `(ip.src == 192.168.1.1) and (tcp.port == 80)`.
3. **Right-Click for Efficiency**:
   - The right-click menu often provides shortcuts to create and apply filters without manually writing queries.
