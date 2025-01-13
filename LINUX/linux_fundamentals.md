
### Key Notes on Linux Basics  

#### **Where is Linux Used?**  
- Powers various systems:  
  - Websites, car systems, Point of Sale (PoS), critical infrastructure like traffic lights.  
- Lightweight and open-source.  

#### **Flavors of Linux**  
- Linux is an umbrella term for various UNIX-based OSs (distributions).  
- Popular Distributions:  
  - **Ubuntu**: Versatile, can be a server or desktop.  
  - **Debian**: Similar to Ubuntu, stable and widely used.  
- Lightweight, but may lack a GUI (Graphical User Interface).  
- **Terminal**: Main interface for interaction.  

#### **Essential Linux Commands**  

1. **Basic Commands**  
   - `echo`: Outputs provided text. Example: `echo "Hello!"`.  
   - `whoami`: Displays the current logged-in user.  

2. **Navigating the Filesystem**  
   - `ls`: Lists files and folders in the current directory.  
   - `cd`: Changes directory. Example: `cd Pictures`.  
   - `pwd`: Prints the full path of the current working directory.  

3. **File Interaction**  
   - `cat`: Displays contents of a file. Example: `cat todo.txt`.  

4. **Finding Files**  
   - `find`: Searches for files.  
     - By name: `find -name passwords.txt`.  
     - By type: `find -name *.txt` (find all `.txt` files).  

5. **Searching File Contents**  
   - `grep`: Searches for specific content in a file. Example:  
     - `grep "IP_Address" access.log`.  

#### **Operators in Linux**  

1. **& (Background Execution)**  
   - Runs commands in the background.  
     - Example: `cp largefile &`.  

2. **&& (Chained Commands)**  
   - Runs multiple commands sequentially if the first is successful.  
     - Example: `command1 && command2`.  

3. **> (Output Redirector)**  
   - Redirects command output to a file (overwrites existing content).  
     - Example: `echo "hello" > file.txt`.  

4. **>> (Append Redirector)**  
   - Appends command output to the end of a file without overwriting.  
     - Example: `echo "world" >> file.txt`.  

#### **Pro Tips**  
- Use `ls <folder_name>` to list the contents of a specific folder without navigating to it.  
- Combine commands for efficiency. Example: `cat /path/to/file`.  
- Use `find` and `grep` to automate file searching and content inspection.

---
---

**Linux Basics: SSH, File Operations, and Directory Structure**

---

### **1. Secure Shell (SSH)**
**Definition:**
- SSH (Secure Shell) is a protocol for secure communication between devices. It encrypts data during transmission.

**Key Features:**
- Execute commands remotely.
- Encrypted data transfer.

**Usage:**
- Syntax: `ssh username@IP_address`
- Example:
  ```bash
  ssh tryhackme@192.168.1.1
  ```
- Username: `tryhackme`
- Password: `tryhackme`

**Important Notes:**
- Typing the password does not show feedback in the terminal.
- SSH prompts to trust the host on the first login.

---

### **2. Common Linux Commands**

#### **File and Folder Operations**
| Command  | Full Name         | Purpose                       |
|----------|-------------------|-------------------------------|
| `touch`  | Create File       | Creates an empty file         |
| `mkdir`  | Make Directory    | Creates a new directory       |
| `cp`     | Copy              | Copies a file or folder       |
| `mv`     | Move              | Moves or renames a file/folder|
| `rm`     | Remove            | Deletes files or folders      |
| `file`   | File Type Checker | Determines file type          |

**Examples:**
- Create a file:
  ```bash
  touch filename
  ```
- Create a folder:
  ```bash
  mkdir foldername
  ```
- Copy a file:
  ```bash
  cp sourcefile destinationfile
  ```
- Move/Rename a file:
  ```bash
  mv oldname newname
  ```
- Delete a file:
  ```bash
  rm filename
  ```
- Delete a folder recursively:
  ```bash
  rm -R foldername
  ```
- Determine file type:
  ```bash
  file filename
  ```

### **3. Exploring Linux Permissions**
**File Permissions Format:**
- Example: `-rw-r--r--`
- Structure: `[type][owner][group][others]`
  - `r`: Read
  - `w`: Write
  - `x`: Execute

**Switching Users:**
- Syntax: `su username`
- Example:
  ```bash
  su user2
  Password:
  ```
- To inherit the user’s environment:
  ```bash
  su -l username
  ```

### **4. Linux Directory Overview**

#### **Important Directories**

1. **/etc**
   - Purpose: Stores system files and configurations.
   - Examples:
     - `passwd`: Stores user account information.
     - `shadow`: Stores encrypted passwords.
     - `sudoers`: Manages sudo permissions.

2. **/var**
   - Purpose: Contains variable data frequently accessed or written by the system.
   - Examples:
     - `/var/log`: Stores log files.
     - `/var/tmp`: Temporary files.

3. **/root**
   - Purpose: Home directory for the `root` user.

4. **/tmp**
   - Purpose: Stores temporary data cleared after system reboot.
   - Note: All users can write to this folder.

### **5. Tips for Command Usage**
- **Man Pages:**
  - Access manual pages for any command: `man command_name`
  - Example:
    ```bash
    man ls
    ```
- **Help Option:**
  - Check available flags and switches: `command --help`
  - Example:
    ```bash
    ls --help
    ```

---
---




## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
