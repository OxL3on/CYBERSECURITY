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


