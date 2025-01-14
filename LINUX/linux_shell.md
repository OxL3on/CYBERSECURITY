### **LINUX SHELL**

1. **CLI vs. GUI:**
   - **GUI:** Easy, user-friendly, requires clicks but less control.  
   - **CLI:** Text-based, efficient, resource-friendly, gives more control.  

2. **Shells in Linux:**
   - **Shell:** Acts as a bridge between you and the OS.  
   - Examples: **Bash, Zsh, Fish**.  

3. **Analogy:**
   - **GUI:** Ordering food from a menu, less effort but limited options.  
   - **CLI:** Cooking in the kitchen (OS) with recipes (commands) for full control.  

4. **Why Use CLI?**
   - More **power** and **control**.  
   - Performs tasks faster and automates processes.  
   - Preferred by professionals for **advanced operations**.  

5. **Shell Scripting:**
   - Automates repetitive tasks efficiently.  
   - Combines multiple commands for complex processes.  

6. **CLI in Hacking:**  
   - Common in hacking for precision, control, and efficiency.  
   - Seen in movies for advanced operations.  

### **Remember:**
- CLI is key to mastering Linux.  
- Practice basic Linux commands (`ls`, `cd`, `cp`, etc.).  
- Explore and write shell scripts for automation.

---
---


### **Types of linux shell**

1. **Default Shell:**
   - Most Linux distributions use **Bash** (Bourne Again Shell) as the default shell.

2. **Basic Commands:**
   - **pwd:** Prints the current working directory.
     ```bash
     user@ubuntu:~$ pwd
     ```
     Output: `/home/user`

   - **cd:** Changes the directory.
     ```bash
     user@ubuntu:~$ cd Desktop
     ```

   - **ls:** Lists the contents of a directory.
     ```bash
     user@ubuntu:~$ ls
     ```
     Output: `Desktop Documents Downloads Music Pictures Public Templates Videos`

   - **cat:** Displays the contents of a file.
     ```bash
     user@ubuntu:~$ cat filename.txt
     ```
     Output: 
     ```
     this is a sample file
     this is the second line of the file
     ```

3. **grep Command:**
   - Searches for specific words or patterns in a file.
     ```bash
     user@ubuntu:~$ grep THM dictionary.txt
     ```
     Output: `The flag is THM`

4. **Key Concept:**
   - Shell commands are efficient for navigating and manipulating files/directories in Linux.  
   - Practice these basic commands to build familiarity.
  
---
---


### **Types of Linux Shells**

#### **1. Checking and Switching Shells:**
- **Check current shell:**
  ```bash
  echo $SHELL
  ```
- **List available shells:**
  ```bash
  cat /etc/shells
  ```
- **Switch to another shell:**
  ```bash
  shell_name  # e.g., zsh
  ```
- **Change default shell:**
  ```bash
  chsh -s /path/to/shell  # e.g., chsh -s /usr/bin/zsh
  ```

#### **2. Popular Linux Shells and Features:**

| Feature              | Bash (Bourne Again Shell)           | Fish (Friendly Interactive Shell)         | Zsh (Z Shell)                            |
|----------------------|------------------------------------|------------------------------------------|------------------------------------------|
| **Scripting**         | Widely compatible with extensive docs | Limited scripting features                 | Advanced scripting with extra features   |
| **Tab Completion**    | Basic                            | Advanced with suggestions                 | Extendable with plugins                 |
| **Customization**     | Basic                            | Good customization through tools          | Advanced customization (e.g., oh-my-zsh)|
| **User-Friendliness** | Less user-friendly but widely used | Most user-friendly                        | User-friendly with customization         |
| **Syntax Highlighting** | Not available                   | Built-in                                 | Plugins required                         |


#### **3. Shell Highlights:**
- **Bash:**
  - Default in most Linux distributions.
  - Features tab completion and command history (`history` command).
- **Fish:**
  - Beginner-friendly with auto spell correction.
  - Built-in syntax highlighting and cool themes.
- **Zsh:**
  - Modern shell combining features of previous shells.
  - Supports plugins for extensive customization (e.g., `oh-my-zsh`).

#### **4. Selecting a Shell:**
- Choose based on your needs:
  - **Bash:** Traditional, widely compatible scripting.
  - **Fish:** For user-friendly and visually appealing features.
  - **Zsh:** For advanced users who want customizations and scripting power.
