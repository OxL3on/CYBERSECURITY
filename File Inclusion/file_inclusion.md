### File Inclusion:

**What is File Inclusion?**  
File inclusion refers to vulnerabilities in web applications that allow an attacker to include files, typically through manipulated input parameters. These vulnerabilities can result in:  
- **Local File Inclusion (LFI):** Reading files already present on the server.  
- **Remote File Inclusion (RFI):** Including files from an external server.  
- **Directory Traversal:** Accessing unintended files by navigating directories.  

These issues arise when web applications retrieve and display files based on user input, such as images or documents. For example, consider the URL:  
```
http://webapp.thm/get.php?file=userCV.pdf
```
Here, the `file` parameter specifies which file to retrieve. If this input isn't properly validated, attackers can manipulate it to include unintended files.


### Why Do File Inclusion Vulnerabilities Happen?  
These vulnerabilities often stem from:  
1. **Poor Input Validation:** User input isn't sanitized or restricted, allowing attackers to pass malicious input.  
2. **Dynamic File Inclusion in Code:** Code written to dynamically include files (e.g., PHP's `include()` or `require()`) can be misused if improperly secured.  


### Risks of File Inclusion  
Exploiting file inclusion vulnerabilities can have severe consequences:  
- **Data Leakage:** Attackers can access sensitive files such as source code, credentials, or system configuration files.  
- **Remote Command Execution (RCE):** If attackers can upload files to the server, they might combine file inclusion with malicious scripts to execute commands remotely.  

For example, an attacker could retrieve system files like `/etc/passwd` (on Linux) or `C:\Windows\System32\config` (on Windows) to gather sensitive information.  

---
---


