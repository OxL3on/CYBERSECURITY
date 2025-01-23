
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


