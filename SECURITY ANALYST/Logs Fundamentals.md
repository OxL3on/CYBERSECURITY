# Logs Fundamentals



### Introduction to Logs

**Main Topic:**  
**Logs** are digital footprints of activities on a system, serving as critical evidence for security monitoring, incident investigation, troubleshooting, and compliance.


### **Key Points:**

1. **What Are Logs?**  
   - Logs record all activities (normal or malicious) on a system.  
   - They act as **digital traces** that help identify how an attack happened or who was behind it.  

2. **Use Cases of Logs:**  
   - **Security Events Monitoring:** Detect unusual behavior in real-time.  
   - **Incident Investigation & Forensics:** Provide detailed information about incidents for root cause analysis.  
   - **Troubleshooting:** Help diagnose and fix system/application errors.  
   - **Performance Monitoring:** Offer insights into application performance.  
   - **Auditing & Compliance:** Create activity trails for audits and regulatory requirements.  

3. **Why Logs Matter:**  
   - Even clever attackers leave traces, and logs capture these clues.  
   - Example: In a snowy cabin theft, footprints, damaged doors, and CCTV footage help solve the case. Similarly, logs help piece together digital attacks.  


**-----**  
Imagine you’re investigating a stolen bike:  
- **Footprints in the snow = Logs** showing suspicious activity.  
- **Broken lock = System error logs** indicating unauthorized access.  
- **CCTV footage = Application logs** capturing the attacker’s actions.  
By analyzing these clues (logs), you can figure out how the thief operated and even identify them.  

In cyber security:  
- Logs are like **breadcrumbs** left by attackers or system events.  
- They help answer: What happened? When? How? And sometimes, who did it?  


**Remembering Tip:**  
Think of logs as a **trail of breadcrumbs**:  
- They show where someone (or something) has been.  
- Use them to retrace steps during investigations or detect anomalies in real-time.  

---
---


### Types of Logs

**Main Topic:**  
Logs are categorized into different types based on the information they provide, making it easier to investigate specific issues or incidents.


### **Key Points:**

1. **Why Categorize Logs?**  
   - Logs contain **numerous events** across categories.  
   - Sorting logs by type helps focus on relevant data for investigations.  

2. **Types of Logs and Their Uses:**  
   - **System Logs:**  
     - Track OS-related activities.  
     - Examples: Startup/shutdown, driver loading, system errors.  

   - **Security Logs:**  
     - Record security-related events.  
     - Examples: Logins, policy changes, user account modifications.  

   - **Application Logs:**  
     - Capture app-specific activities.  
     - Examples: User interactions, updates, errors.  

   - **Audit Logs:**  
     - Provide detailed records for compliance and monitoring.  
     - Examples: Data access, system changes, user activity.  

   - **Network Logs:**  
     - Monitor incoming/outgoing traffic.  
     - Examples: Firewall logs, connection details.  

   - **Access Logs:**  
     - Track resource access (e.g., web servers, databases).  
     - Examples: Who accessed what and when.  

3. **Log Analysis:**  
   - Extract valuable data from logs to detect abnormal or suspicious activities.  
   - Manual or automated techniques are used since reviewing raw logs is impractical.  


**-----**  
Imagine you’re a librarian trying to find a misplaced book:  
- Instead of searching every shelf, you check logs like:  
  - **Borrowing logs** (who took the book).  
  - **Shelf logs** (where it should be).  
  - **Visitor logs** (who was in the library).  

In cyber security:  
- Logs are like **organized shelves** of information.  
- For example:  
  - Check **Security Logs** for login issues.  
  - Use **Network Logs** for suspicious traffic.  
  - Review **Access Logs** to see who accessed sensitive files.  


**Remembering Tip:**  
Think of logs as **folders in a filing cabinet**:  
- Each folder (log type) contains specific info.  
- Pick the right folder to solve your problem!  

---
---


### Windows Event Logs Analysis

**Main Topic:**  
Windows Event Logs record system, application, and security activities. **Event Viewer** is a built-in tool to view and analyze these logs using **Event IDs** for specific activities.


### **Key Points:**

1. **Types of Windows Logs:**  
   - **Application Logs:** Track app-related activities (e.g., errors, warnings).  
   - **System Logs:** Record OS operations (e.g., startup/shutdown, driver issues).  
   - **Security Logs:** Log security events (e.g., logins, account changes).  

2. **Key Fields in Event Logs:**  
   - **Description:** Details about the activity.  
   - **Log Name:** The category of the log (e.g., Security, System).  
   - **Logged:** Timestamp of the event.  
   - **Event ID:** Unique identifier for specific activities.  

3. **Important Event IDs:**  
   - **4624:** Successful login.  
   - **4625:** Failed login attempt.  
   - **4634:** Successful logout.  
   - **4720:** User account created.  
   - **4724:** Password reset attempt.  
   - **4722:** Account enabled.  
   - **4725:** Account disabled.  
   - **4726:** Account deleted.  

4. **Using Event Viewer:**  
   - Open via **Start > Event Viewer**.  
   - Navigate to **Windows Logs** to see categories (e.g., Security, System).  
   - Use **Filter Current Log** to search by specific **Event IDs**.  


**-----**  
Imagine you’re a detective solving a mystery:  
- **Event Logs = Clues** left behind by activities on the system.  
- **Event IDs = Labels** that tell you what each clue means.  
  - Example: Searching for **Event ID 4624** helps you find all successful logins.  
- **Event Viewer = Your magnifying glass** to filter and analyze clues quickly.  

In cyber security:  
- Use **Event Viewer** to investigate suspicious activities.  
- Example: If you suspect unauthorized access, check **Event ID 4625** (failed logins).  


**Remembering Tip:**  
Think of **Event IDs** as **codes for clues**:  
- **4624 = Someone logged in.**  
- **4625 = Someone tried and failed to log in.**  
Use **Event Viewer** to filter logs like searching for keywords in a book!  

---
---



### Web Server Access Logs Analysis

**Main Topic:**  
Web server access logs record all requests made to a website, including details like IP addresses, timestamps, request types, and status codes. Tools like `cat`, `grep`, and `less` help analyze these logs manually in Linux.


### **Key Points:**

1. **What’s in a Web Server Log?**  
   - **IP Address:** Who made the request (e.g., `172.16.0.1`).  
   - **Timestamp:** When the request was made (e.g., `[06/Jun/2024:13:58:44]`).  
   - **Request Details:**  
     - **HTTP Method:** What action was requested (e.g., `GET`, `POST`).  
     - **URL:** The resource accessed (e.g., `/products`).  
   - **Status Code:** Server’s response (e.g., `200` = Success, `404` = Not Found).  
   - **User-Agent:** Info about the user’s device and browser.  

2. **Log Rotation:**  
   - Logs are split into separate files for specific timeframes to avoid clutter.  
   - Use `cat` to combine multiple log files if needed:  
     ```bash
     cat access1.log access2.log > combined_access.log
     ```

3. **Command Line Tools for Log Analysis:**  
   - **`cat`:** Display log file contents.  
     ```bash
     cat access.log
     ```  
   - **`grep`:** Search for specific patterns (e.g., an IP address):  
     ```bash
     grep "192.168.1.1" access.log
     ```  
   - **`less`:** View logs page by page for easier manual analysis:  
     ```bash
     less access.log
     ```  
     - Use `/pattern` to search within `less`.  
     - Navigate with `n` (next) and `N` (previous).  


**-----**  
Imagine you’re a store owner reviewing security footage:  
- **Logs = Security camera footage** of every visitor.  
- **IP Address = Visitor’s face** (who they are).  
- **Timestamp = Time of visit** (when they came).  
- **Request = What they did** (e.g., browsed products, tried to enter restricted areas).  
- **Status Code = Outcome** (e.g., success, failure).  

In cyber security:  
- Use `grep` to find suspicious IPs (e.g., repeated failed login attempts).  
- Use `less` to review logs page by page and spot unusual patterns.  


**Remembering Tip:**  
Think of logs as a **guestbook** at a party:  
- Each entry tells you who came, when, and what they did.  
Use tools like `cat`, `grep`, and `less` to skim through or search for specific guests!  
