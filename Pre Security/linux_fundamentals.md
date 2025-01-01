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


## Acknowledgment  
The content in this repository is inspired by the 'Pre-Security' room on [TryHackMe](https://tryhackme.com/r/path/outline/presecurity). Full credit to TryHackMe for creating the material used as a learning resource.  
