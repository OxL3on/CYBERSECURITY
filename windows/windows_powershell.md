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

#### **What is PowerShell?**
- **Definition**: PowerShell is a cross-platform task automation solution by Microsoft, combining a command-line shell, scripting language, and configuration management framework.
- **Key Features**:
  - Object-oriented: Handles structured data with properties and methods.
  - Built on .NET Framework (later versions use .NET Core for cross-platform compatibility).
  - Initially for Windows, now supports macOS and Linux.

#### **History of PowerShell**
- **Development Motivation**:
  - Addressed limitations of `cmd.exe` and batch files for complex administrative tasks.
  - Inspired by Unix’s text-file approach but used object-oriented design for Windows APIs.
- **Key Milestones**:
  - 2006: Initial release, exclusive to Windows.
  - 2016: Launch of PowerShell Core, open-source and cross-platform.

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

#### **Practical Application in the Lab**
1. **Start the Machine**: Use the provided AttackBox environment.
2. **Connect via SSH**:
   - Use `Remmina` and provide credentials:  
     - Username: `captain`  
     - Password: `JollyR0ger#`  
     - IP: `MACHINE_IP`.
3. **Launch PowerShell**:
   - From Command Prompt, type `powershell`.

---
---



