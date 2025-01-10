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

