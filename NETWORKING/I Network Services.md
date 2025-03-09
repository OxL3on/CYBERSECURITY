# Network Services I



### SMB Basics

**Main Topic:** SMB (Server Message Block) lets computers share stuff like files and printers over a network.  
- **What It Does:** Connects clients (your PC) to servers for file access, printing, etc.  
- **How It Works:** Client asks, server answers—uses TCP/IP or other network tricks.  

**Example:** Imagine your PC asking the office server, “Hey, can I grab that shared doc?” SMB makes it happen!

**Cool Fact:** Windows (since ‘95) and Samba (for Unix) run SMB.

**Remembering Tip:** Think of SMB as a “network librarian”—hands out files and printer access like books!

---


### Enumerating SMB

**Main Topic:** Enumeration digs up info on SMB to find attack openings.  
- **What’s Enumeration?** Gathering details (users, shares, etc.) to plan a smart attack.  
- **SMB Focus:** SMB shares on servers might hold juicy files—great starting point.

**Steps:**  
1. **Port Scan:** Use Nmap to spot open ports and services on the target.  
2. **Enum4Linux:** Tool to grab SMB info fast (on AttackBox or GitHub).  
   - Run: `enum4linux -a MACHINE_IP`—gets users, shares, passwords, all the basics.

**Example:** Scan a server, find a share with “secret_plans.txt”—bingo!

**Remembering Tip:** Think of enumeration as “snooping through a server’s desk”—Enum4Linux is your flashlight!

---


