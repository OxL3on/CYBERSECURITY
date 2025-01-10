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



