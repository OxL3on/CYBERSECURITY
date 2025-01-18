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


