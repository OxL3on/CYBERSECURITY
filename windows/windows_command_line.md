### Command Prompt and System Information Commands

#### **1. Understanding the Windows Path**
- **Command Execution Location**: Commands are executed only in directories listed in the **Windows Path**.
- **Check Path**: Use the `set` command in the Command Prompt to view environment variables, including the Path.
  - Example:
    ```plaintext
    C:\>set
    Path=C:\Windows\system32;C:\Windows;...
    ```

#### **2. Basic Commands**
- **Check OS Version**: Use the `ver` command.
  - Example:
    ```plaintext
    C:\>ver
    Microsoft Windows [Version 10.0.17763.1821]
    ```
- **Get Detailed System Information**: Use the `systeminfo` command.
  - Displays:
    - OS Name and Version
    - Host Name
    - Processor and Memory details
  - Example snippet:
    ```plaintext
    C:\>systeminfo
    Host Name:                 WIN-SRV-2019
    OS Name:                   Microsoft Windows Server 2019 Datacenter
    ```

#### **3. Enhancing Output Visibility**
- **Pipe Command Output**: If the output is too long, use `| more` to view it page by page.
  - Example:
    ```plaintext
    C:\>driverquery | more
    ```
  - **Controls**:
    - **Space Bar**: Move to the next page.
    - **CTRL + C**: Exit.

#### **4. Useful Commands**
- **`help`**: Provides help for specific commands.
  - Example: `help systeminfo`
- **`cls`**: Clears the Command Prompt screen.

#### **Example Use Case**
Imagine you want to find out system details but the list is too long:
1. Run `systeminfo | more` to review it page by page.
2. Exit when you find the information you need using **CTRL + C**.

---
---


### Networking Commands 

#### **1. View Network Configuration**
- **Basic Info**: Use `ipconfig` to see:
  - **IPv4 Address**: Your device's unique address in the network.
  - **Subnet Mask**: Defines the network segment.
  - **Default Gateway**: Router address for external communication.
  - Example:
    ```plaintext
    C:\>ipconfig
    IPv4 Address. . . . . : 10.10.230.237
    Subnet Mask . . . . . : 255.255.0.0
    Default Gateway . . . : 10.10.0.1
    ```

- **Detailed Info**: Use `ipconfig /all` for advanced details like:
  - **DHCP Enabled**: Indicates if your IP is auto-assigned.
  - **DNS Servers**: Servers resolving domain names.
  - **Physical Address**: MAC address of the adapter.

#### **2. Network Troubleshooting Commands**
- **Check Connectivity**: Use `ping target_name` to verify if a server is reachable.
  - Sends packets and measures response times.
  - Example:
    ```plaintext
    C:\>ping example.com
    Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
    ```
- **Trace Network Route**: Use `tracert target_name` to trace the path packets take to the target.
  - Example:
    ```plaintext
    C:\>tracert example.com
    Hop 1: ec2-3-248-240-3.eu-west-1.compute.amazonaws.com [3.248.240.3]
    ```
- **Domain Name Resolution**: Use `nslookup` to find the IP address of a domain.
  - Default DNS server: `nslookup example.com`.
  - Specific DNS server: `nslookup example.com 1.1.1.1`.

#### **3. Monitor Network Connections**
- **Current Connections**: Use `netstat` to see:
  - Active connections.
  - Listening ports.
  - Example:
    ```plaintext
    C:\>netstat
    Proto  Local Address        Foreign Address      State
    TCP    10.10.230.237:22     ip-10-11-81-126:53486  ESTABLISHED
    ```

- **Advanced Options**:
  - `-a`: Show all connections and listening ports.
  - `-b`: Show the program linked to each connection.
  - `-o`: Show Process ID (PID) for each connection.
  - Combine options: `netstat -abon`.

#### **Example Use Case**
Imagine your internet is slow:
1. Use `ping example.com` to check connectivity and response times.
2. Use `tracert example.com` to trace delays across routers.
3. Use `netstat -abon` to check which processes are consuming network resources.


---
---


### File and Disk Management

#### **Working with Directories**
1. **Current Directory:**
   - `cd` → Displays the current drive and directory.

2. **List Files/Directories:**
   - `dir` → Lists contents of the current directory.
   - `dir /a` → Includes hidden/system files.
   - `dir /s` → Lists files in all subdirectories.

3. **Directory Structure:**
   - `tree` → Displays a visual representation of subdirectories.

4. **Change Directory:**
   - `cd target_directory` → Moves to the specified directory.
   - `cd ..` → Moves up one level.
   - `cd \` → Moves to the root directory.

5. **Create/Delete Directories:**
   - `mkdir directory_name` → Creates a new directory.
   - `rmdir directory_name` → Deletes an empty directory.

#### **Working with Files**
1. **View File Contents:**
   - `type file.txt` → Displays file content.
   - `more file.txt` → Paginates file content (use `Spacebar` for the next page).

2. **Copy Files:**
   - `copy source destination` → Copies a file to a new location.
   - Example: `copy test.txt test2.txt`

3. **Move Files:**
   - `move source destination` → Moves a file.
   - Example: `move test2.txt ..` (Moves `test2.txt` to the parent directory).

4. **Delete Files:**
   - `del file_name` or `erase file_name` → Deletes a file.

5. **Wildcard Character:**
   - `copy *.ext destination` → Copies all files with the specified extension to the destination.
   - Example: `copy *.md C:\Markdown`

#### Example Workflow
- View all directories: `dir`
- Create a directory: `mkdir backup`
- Copy a file: `copy test.txt backup\test.txt`
- Move a file: `move backup\test.txt .`
- Delete a file: `del test.txt`

---
---


### Task and Process Management

#### **Listing Running Processes**
1. **View All Processes:**
   - `tasklist` → Displays all running processes with details (Image Name, PID, Session, Memory Usage).

2. **Filter Processes:**
   - `tasklist /FI "imagename eq process_name"` → Filters by process name.
     - Example: `tasklist /FI "imagename eq sshd.exe"`
   - You can use multiple filters; refer to `tasklist /?` for options.

####3 **Killing Processes**
1. **Terminate a Process by PID:**
   - `taskkill /PID target_pid`
     - Example: `taskkill /PID 4567`

2. **Terminate All Processes by Name:**
   - `taskkill /IM process_name /F`
     - Example: `taskkill /IM sshd.exe /F`
   - `/F` forces the termination of the process.

#### **Examples**
- **List Processes:**  
  ```bash
  tasklist
  ```

- **Filter for a Specific Process:**  
  ```bash
  tasklist /FI "imagename eq notepad.exe"
  ```

- **Kill a Process by PID:**  
  ```bash
  taskkill /PID 1234
  ```

- **Force Kill by Name:**  
  ```bash
  taskkill /IM chrome.exe /F
  ```

#### **Extra**
- Always check the process details with `tasklist` before terminating.
- Use `/F` cautiously as it forces termination and may cause system instability if critical processes are killed. 


