## Windows Fundamentals Notes

### Overview of Windows OS
- **History & Versions**:
  - Windows OS debuted in 1985 and is the most widely used OS.
  - Popular versions: Windows XP (long-lasting), Vista (poor reception), Windows 7 (widely adopted), Windows 8.x (short-lived), Windows 10, and Windows 11 (current for end-users).
  - Server versions include Windows Server 2019.
- **File System**:
  - Modern Windows uses **NTFS** (New Technology File System).
  - NTFS supports:
    - Files >4GB
    - Permissions (Full control, Modify, Read & Execute, etc.)
    - Compression and Encryption (EFS).
  - Older systems used FAT16/FAT32 or HPFS.

### Graphical User Interface (GUI) Components
- **Desktop**:
  - Quick access to shortcuts and folders.
  - Customize via right-click context menu (e.g., Display settings, Personalize).
  - Change wallpaper, themes, and resolution.
- **Start Menu**:
  - Access to apps, files, and utilities.
  - Divided into sections:
    1. Account and session controls (lock, sign out, settings, etc.).
    2. Recently added and installed apps (alphabetical listing).
    3. Tiles for pinned apps (can customize via right-click).
- **Taskbar**:
  - Displays open applications and pinned items.
  - Hovering provides previews and tooltips.
  - Customize via right-click context menu.
- **Notification Area**:
  - Located bottom-right, displays date/time, volume, and network icons.
  - Manage icons in Taskbar settings.

### File System Basics
- **System Folders**:
  - The Windows folder (default: `C:\Windows`) contains critical OS files.
  - `System32` holds essential system files (avoid altering).
- **Environment Variables**:
  - `%windir%` points to the Windows directory.
  - Variables store OS-specific information (e.g., paths, temp folder locations).
- **Alternate Data Streams (ADS)**:
  - Specific to NTFS, allows files to contain additional streams of data.
  - Often used by malware for hiding data but also for metadata like download origins.

### User Accounts
- **Types**:
  - **Administrator**: Full system access.
  - **Standard User**: Limited to personal files/folders.
- **Account Management**:
  - Use `lusrmgr.msc` for Local Users and Groups Management.
  - Add users to groups to inherit permissions.
- **User Account Control (UAC)**:
  - Protects against unauthorized system changes.
  - Prompts for admin credentials when elevated permissions are needed.

### Settings and Control Panel
- **Settings Menu**:
  - Introduced in Windows 8 for touch-friendly access.
  - Used for common configurations (e.g., display, network settings).
- **Control Panel**:
  - Legacy tool for advanced settings (e.g., adapter settings, system configurations).
  - Some actions in Settings redirect to Control Panel.

### Task Manager
- **Purpose**:
  - Displays running apps/processes and system resource usage (CPU, RAM).
- **Access**:
  - Right-click Taskbar > Select Task Manager.
- **Views**:
  - Simple View: Limited info.
  - Expanded View: Detailed breakdown of processes and performance.

### Tips and Resources
- **Shortcuts**:
  - Right-click for quick access to properties and actions.
  - Use the Run dialog (`Win + R`) for direct access to tools (e.g., `lusrmgr.msc`).
- **Resources**:
  - [Microsoft Documentation on NTFS, FAT, and HPFS](https://learn.microsoft.com).
  - [MalwareBytes on ADS](https://www.malwarebytes.com).
  - Core Windows Processes: Refer to relevant learning rooms for details.

---
---


### Notes on System Configuration Utility (MSConfig) and Related Tools

#### **System Configuration Utility (MSConfig)**
- **Purpose**: Advanced troubleshooting and diagnosing startup issues.
- **Access**: Requires local administrator rights.
- **Tabs**:
  1. **General**: Choose startup modes: Normal, Diagnostic, or Selective.
  2. **Boot**: Configure boot options.
  3. **Services**: List all services, running or stopped.
  4. **Startup**: Redirects to Task Manager for managing startup items.
  5. **Tools**: Provides access to various system tools.

#### **Tools Overview**
1. **User Account Control (UAC)**:
   - Adjusts UAC settings but turning it off is not recommended.

2. **Computer Management (compmgmt)**:
   - **Task Scheduler**: Automate tasks like running scripts or apps on a schedule.
   - **Event Viewer**: Logs system events (e.g., errors, warnings, informational logs).
   - **Shared Folders**: View shared resources, connected users, and open files.
   - **Performance Monitor (perfmon)**: Real-time or logged system performance data.
   - **Device Manager**: Configure or disable hardware devices.

3. **Storage**:
   - **Disk Management**:
     - Setup new drives, extend/shrink partitions, assign/change drive letters.

4. **Services and Applications**:
   - Manage and view properties of background services.
   - **WMI Control**: Manages WMI services, superseded by PowerShell.

#### **Key Tools**
1. **System Information (msinfo32)**:
   - Displays hardware, components, and software details.
   - Useful for diagnosing hardware or software issues.

2. **Resource Monitor (resmon)**:
   - Monitors CPU, memory, disk, and network usage.
   - Includes advanced filtering for process analysis.

3. **Command Prompt (cmd)**:
   - **Basic Commands**:
     - `hostname`: Displays computer name.
     - `whoami`: Displays logged-in user.
     - `ipconfig`: Shows network settings.
     - `cls`: Clears the screen.
   - **Advanced Commands**:
     - `netstat`: Displays protocol stats and network connections.
     - `net help`: Displays help for `net` sub-commands (e.g., `user`, `share`, `session`).

4. **Windows Registry (regedit)**:
   - Stores system configuration data (e.g., user profiles, hardware info).
   - **Warning**: Modifying the registry can impact system functionality.

#### **Key Notes**:
- Always ensure admin rights before accessing advanced tools.
- Refer to built-in help manuals (e.g., `command /?`) for syntax and options.
- Exercise caution when modifying system settings, especially the registry.
- Use Task Scheduler and Event Viewer for task automation and issue diagnostics.
- Familiarize yourself with tools like Resource Monitor and Performance Monitor for advanced troubleshooting.


---
---

