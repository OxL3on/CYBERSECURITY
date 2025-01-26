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


### Path Traversal:

#### **What is Path Traversal?**  
Path Traversal (or Directory Traversal) is a web vulnerability that allows attackers to access files and directories outside the intended root directory of a web application. This vulnerability occurs due to **poor input validation** and can lead to unauthorized access to sensitive files.


#### **How Does Path Traversal Work?**  
When web applications handle file requests dynamically (e.g., using functions like PHP's `file_get_contents()`), attackers can manipulate URL parameters to traverse directories. The typical payload involves using `../` to move up one directory at a time.

**Example Attack on Linux:**  
Target URL:  
```
http://webapp.thm/get.php?file=userCV.pdf
```

Malicious payload:  
```
http://webapp.thm/get.php?file=../../../../etc/passwd
```

Here:  
- `../../../../` moves up directories until reaching the root `/`.
- `/etc/passwd` is a sensitive file that contains user account information.

---

#### **Path Traversal on Windows**  
On Windows systems, attackers use Windows-style paths like:  
```
http://webapp.thm/get.php?file=../../../../boot.ini
```
or  
```
http://webapp.thm/get.php?file=../../../../windows/win.ini
```


#### **Key Files to Target During Testing**  
Below are common sensitive files across Linux and Windows systems:

| **Location**                  | **Description**                                                                 |
|-------------------------------|---------------------------------------------------------------------------------|
| `/etc/issue`                  | System identification message before the login prompt.                          |
| `/etc/profile`                | System-wide default variables and configurations.                              |
| `/proc/version`               | Version of the Linux kernel.                                                   |
| `/etc/passwd`                 | User account details.                                                          |
| `/etc/shadow`                 | Encrypted passwords (requires root privileges).                                |
| `/root/.bash_history`         | Command history for the root user.                                             |
| `/var/log/dmesg`              | System messages logged during startup.                                         |
| `/var/mail/root`              | Emails for the root user.                                                      |
| `/root/.ssh/id_rsa`           | Private SSH keys for the root user.                                            |
| `/var/log/apache2/access.log` | Logs of accessed requests for the Apache server.                               |
| `C:\boot.ini`                 | Boot options for systems with BIOS firmware.                                   |


#### **Mitigation and Prevention**  
1. **Input Validation:**  
   - Sanitize user inputs.
   - Only allow predefined, safe file paths.

2. **Restrict Access:**  
   - Use a secure base directory and limit file access within it.  
   - Disable unnecessary features like directory indexing.  

3. **Code Practices:**  
   - Avoid concatenating user input into file paths.
   - Implement allowlists for permitted file names or extensions.  

---
---


