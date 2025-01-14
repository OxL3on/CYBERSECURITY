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
 
---
---


### **Shell Scripting Basics**

#### **1. What is Shell Scripting?**
- A shell script is a set of commands saved in a file with the `.sh` extension.
- Scripts automate repetitive tasks by executing a sequence of commands in one go.

#### **2. Steps to Create and Execute a Script:**
1. **Create a script file:**
   ```bash
   nano script_name.sh
   ```
2. **Start with a shebang (`#!`):**
   - Specifies the interpreter to execute the script.
   ```bash
   #!/bin/bash
   ```
3. **Write your script code.**

4. **Give execution permission:**
   ```bash
   chmod +x script_name.sh
   ```
5. **Run the script:**
   ```bash
   ./script_name.sh
   ```

#### **3. Basic Constructs:**

##### **a) Variables**
- Store values to reuse in the script.
- Example:
  ```bash
  #!/bin/bash
  echo "Enter your name:"
  read name
  echo "Hello, $name!"
  ```

##### **b) Loops**
- Repeat tasks automatically.
- Example (For Loop):
  ```bash
  #!/bin/bash
  for i in {1..5}
  do
      echo "Number: $i"
  done
  ```

##### **c) Conditional Statements**
- Perform tasks based on conditions.
- Example:
  ```bash
  #!/bin/bash
  echo "Enter your name:"
  read name
  if [ "$name" = "Admin" ]; then
      echo "Welcome, Admin!"
  else
      echo "Access Denied!"
  fi
  ```

##### **d) Comments**
- Add explanations to your code.
- Single-line comment:
  ```bash
  # This is a comment
  ```
- Multi-line comments:
  ```bash
  : '
  This is a
  multi-line comment.
  '
  ```

#### **4. Practical Examples:**

##### **Example 1: Greeting Script**
```bash
#!/bin/bash
echo "What is your name?"
read name
echo "Welcome, $name!"
```

##### **Example 2: Loop Example**
```bash
#!/bin/bash
for num in {1..5}
do
    echo "Current number: $num"
done
```

##### **Example 3: Conditional Script**
```bash
#!/bin/bash
echo "Enter your username:"
read username
if [ "$username" = "Admin" ]; then
    echo "Hello, Admin! Access granted."
else
    echo "Access denied."
fi
```

##### **Example 4: With Comments**
```bash
#!/bin/bash

# Prompt the user for their name
echo "Enter your name:"
read name

# Check if the name matches 'Admin'
if [ "$name" = "Admin" ]; then
    echo "Welcome, Admin!"
else
    echo "Access denied."
fi
```

#### **5. Why Use Shell Scripts?**
- **Efficiency:** Automate repetitive tasks.
- **Convenience:** Run multiple commands with a single script.
- **Flexibility:** Combine commands, variables, and logic for complex tasks.

---
---


### **The Locker Script**

```bash
# Defining the Interpreter 
#!/bin/bash 

# Defining the variables
username=""
companyname=""
pin=""

# Defining the loop
for i in {1..3}; do
# Defining the conditional statements
        if [ "$i" -eq 1 ]; then
                echo "Enter your Username:"
                read username
        elif [ "$i" -eq 2 ]; then
                echo "Enter your Company name:"
                read companyname
        else
                echo "Enter your PIN:"
                read pin
        fi
done

# Checking if the user entered the correct details
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
        echo "Authentication Successful. You can now access your locker, John."
else
        echo "Authentication Denied!!"
fi
```


### **Output**
For successful authentication, the user must input all correct details:
```plaintext
Enter your Username:
John
Enter your Company name:
Tryhackme
Enter your PIN:
7385
Authentication Successful. You can now access your locker, John.
```

