### Introduction to Hashes and Hash Cracking

#### **What are Hashes?**

- **Definition**:  
  A **hash** is like a digital fingerprint for data. It takes data of any length and converts it into a fixed-length code using a hashing algorithm.  
  **Purpose**: To mask the original data while keeping a unique representation.

- **Example**:  
  Imagine a magic box that always outputs a 32-character code, no matter what you put inside.  
  - Input: "polo" → MD5 Hash: `b53759f3ce692de7aff1b5779d3964da`  
  - Input: "polomints" → MD5 Hash: `584b6e4f4586e136bc280f27f9c64f3b`  

Even a tiny change in the input drastically changes the hash, ensuring uniqueness.

- **Common Hashing Algorithms**:  
  Examples include **MD4**, **MD5**, **SHA1**, and **NTLM**.

#### **What Makes Hashes Secure?**

- **One-Way Street**:  
  Hashing is a **one-way process**—easy to calculate a hash but nearly impossible to reverse-engineer the original data.

- **Mathematical Roots**:  
  This complexity is tied to a concept in computer science called **P vs NP**:  
  - **P (Polynomial Time)**: Solving the problem (e.g., creating a hash) is manageable and efficient.  
  - **NP (Non-deterministic Polynomial Time)**: Reversing the process (e.g., "un-hashing") is too complex for standard computers to solve in a reasonable time.

#### **How Do Hackers Crack Hashes?**

While un-hashing isn't feasible, hackers use a clever workaround: **dictionary attacks**.  
1. **Dictionary Attack Steps**:  
   - Prepare a list of potential passwords (the "dictionary").  
   - Hash each word using the same algorithm.  
   - Compare each generated hash with the target hash.  

   **If a match is found**, the original password is identified.  

2. **Tool Example**:  
   **John the Ripper** (often called "John") is a powerful tool for performing brute force and dictionary attacks to crack hashes.

#### **Learning Resources**:

- If you're new to cryptography, explore:  
  - **Cryptography Basics Room**  
  - **Public Key Cryptography Basics Room**  

- For hashing, check out the **Hashing Basics Room**.

#### **Key Takeaway**:

Cracking hashes isn't about reversing the process but comparing them against precomputed or dynamically generated hashes. Tools like **Jumbo John** make this process faster and more effective.

---
---



### Setting Up John the Ripper and Wordlists

#### **Tools Needed for This Room**:
1. **Jumbo John**: A powerful, extended version of John the Ripper for hash cracking.  
2. **RockYou Password List**: A large list of common passwords from the 2009 RockYou data breach.

#### **Using Virtual Machines or AttackBox**:
- **Pre-installed Tools**:  
  If you’re using the attached VM or AttackBox, **Jumbo John** is already installed. You don’t need to install it yourself.  

- **How to Check**:  
  Open the terminal and type `john`. If installed, you’ll see a usage guide with a version like `John the Ripper 1.9.0-jumbo-1`.  

#### **Installing Jumbo John**:

1. **On Linux Distributions**:
   - **From Official Repositories**:  
     - Fedora: `sudo dnf install john`  
     - Ubuntu: `sudo apt install john`  
     - Note: These versions may lack Jumbo John’s advanced tools like `zip2john` or `rar2john`.
   - **Building from Source**:  
     For full features, download and build Jumbo John from its official installation guide.

2. **On Windows**:
   - Download the pre-compiled binaries for your system (64-bit or 32-bit). Extract and set it up.

#### **What Are Wordlists?**

- **Definition**:  
  Wordlists are files containing potential passwords used during dictionary attacks.

- **Example**:  
  Imagine a keysmith trying to open a lock by testing every possible key in a box. The **wordlist** is that box of keys.

- **Popular Wordlist Locations**:
  - On **AttackBox** or **Kali Linux**: `/usr/share/wordlists`.  
  - **SecLists Repository**: A collection of wordlists for various purposes.  

#### **RockYou Wordlist**:

- **About RockYou**:  
  A wordlist containing millions of leaked passwords from the 2009 RockYou.com data breach. It’s commonly used for password cracking due to its size and real-world relevance.

- **Getting RockYou**:
  - On **Kali Linux**: Pre-installed in `/usr/share/wordlists`.  
  - From **SecLists Repository**: Found under `/Passwords/Leaked-Databases`.  
  - **Extracting RockYou**: If it’s in `.tar.gz` format, use:  
    ```bash
    tar xvzf rockyou.txt.tar.gz
    ```

---
---

### Cracking Hashes with John the Ripper

#### **Basic Syntax of John the Ripper**  
The general format of a John the Ripper command is:  
```bash
john [options] [file path]
```
- **john**: Starts the tool.  
- **[options]**: Flags and modifiers to customize the cracking process.  
- **[file path]**: Path to the file containing the hash(es) to crack.

#### **Automatic Cracking**  
John can automatically detect hash types and attempt to crack them.  
**Command Syntax**:  
```bash
john --wordlist=[path to wordlist] [path to file]
```
- **--wordlist=**: Specifies the wordlist to use.  
- **Example**:  
  ```bash
  john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
  ```

#### **Identifying Hashes**  
Sometimes, John may not correctly identify the hash format. Use a tool like **hash-identifier** to identify the hash type.  
**Steps**:  
1. Download the tool:  
   ```bash
   wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
   ```
2. Run it:  
   ```bash
   python3 hash-id.py
   ```
3. Enter the hash to get a list of possible formats.  
   **Example Output**:  
   ```
   HASH: 2e728dd31fb5949bc39cac5a9f066498  
   Possible Hashes:  
   [+] MD5  
   [+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))  
   ```

#### **Cracking Specific Formats**  
Once you know the hash format, specify it to John.  
**Command Syntax**:  
```bash
john --format=[format] --wordlist=[path to wordlist] [path to file]
```
- **--format=**: Specifies the hash format to use.  
- **Example**:  
  ```bash
  john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
  ```

#### **Important Notes on Formats**  
- For standard hash types (like MD5), prefix with `raw-`, e.g., `raw-md5`.  
- To list all supported formats:  
  ```bash
  john --list=formats
  ```
- Use `grep` to find a specific format:  
  ```bash
  john --list=formats | grep -iF "md5"
  ```

#### **Practical Example**  

**Scenario**: You have a file named `hash_to_crack.txt` with an MD5 hash. You want to crack it using the **RockYou** wordlist.  
**Steps**:  
1. Identify the hash type:  
   ```bash
   python3 hash-id.py
   ```
   Output: The hash is **MD5**.  

2. Crack the hash:  
   ```bash
   john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
   ```
3. View the results after cracking:  
   ```bash
   john --show hash_to_crack.txt
   ```

### **Analogy**: Cracking Hashes with John  

Imagine you're trying to unlock a treasure chest with a secret code.  
- The **hash** is the locked chest.  
- The **hashing algorithm** (e.g., MD5) is how the lock was made.  
- **John** is your master locksmith who can try different keys (passwords) from a **wordlist** to find the right one.  

By specifying the lock type (`--format`) and giving John a set of keys (`--wordlist`), you’ll quickly crack the chest open and retrieve the treasure (original data).

---
---

### Cracking Windows Authentication Hashes with John the Ripper

#### **Windows Authentication Hashes Overview**
- **NTHash (NTLM)**:  
  - Modern Windows systems use NTHash (commonly referred to as NTLM) to store user and service passwords.  
  - NTLM succeeded the older **LM (LAN Manager)** hashing format.  
  - Stored in the **SAM (Security Account Manager)** database on Windows systems.  

#### **Acquiring NTHashes**
1. **Dump SAM Database**: Extract hashed passwords using tools like Mimikatz or secretsdump.py (from the Impacket suite).  
2. **Extract Active Directory Hashes**: Retrieve hashes from **NTDS.dit** (Active Directory database).  
3. **Pass the Hash**: Instead of cracking, reuse the hash directly for authentication.  

#### **Cracking NTLM Hashes**
1. Identify the hash type as **NTLM** (or **NTHash**) using tools like `hash-identifier`.  
2. Use John the Ripper to crack it.

#### **Practical Example: Cracking NTLM Hashes**

**Scenario**: You have an NTLM hash stored in `ntlm.txt`. The file path is `~/John-the-Ripper-The-Basics/Task05/`.

**Steps**:  

1. **Verify the hash type**:
   Use `hash-identifier` to confirm the hash format.  
   Example hash:  
   ```
   8846f7eaee8fb117ad06bdd830b7586c
   ```
   Output: **NTLM**.

2. **Crack the NTLM hash**:
   Use John with the RockYou wordlist.  
   ```bash
   john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt ~/John-the-Ripper-The-Basics/Task05/ntlm.txt
   ```

3. **Check the results**:
   Once the cracking is complete, view the cracked password with:  
   ```bash
   john --show ~/John-the-Ripper-The-Basics/Task05/ntlm.txt
   ```

#### **Explanation of Commands**
- `--format=nt`: Specifies NTLM hash format.  
- `--wordlist=/usr/share/wordlists/rockyou.txt`: Path to the RockYou wordlist.  

### **Analogy**: Cracking NTLM Hashes  
Imagine the NTLM hash as a **coded lock** on a door.  
- The SAM database is like a **keyring** storing these locks.  
- John is your **locksmith** who tries every possible key (password) from the wordlist (e.g., RockYou) until the lock opens (hash is cracked).  

#### **Additional Notes**  
- Weak password policies can make NTLM hashes vulnerable to brute-force attacks.  
- Cracked passwords can be used for further lateral movement or privilege escalation during penetration testing.  
- If cracking is infeasible, leverage **pass-the-hash** techniques for authentication bypass.

---
---


### Cracking `/etc/shadow` Hashes with John the Ripper

#### **Understanding `/etc/shadow` and `/etc/passwd`**
- **`/etc/shadow`**:  
  Stores hashed passwords and metadata, such as password expiration. Access is restricted to privileged users (e.g., root).  
  Example entry:  
  ```
  root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::
  ```
  - `$6$` indicates the hash uses SHA-512 crypt.  

- **`/etc/passwd`**:  
  Contains user account information, but does not store passwords. It maps usernames to system information.  
  Example entry:  
  ```
  root:x:0:0::/root:/bin/bash
  ```

#### **Combining `/etc/shadow` and `/etc/passwd` with `unshadow`**
To crack `/etc/shadow` hashes, you must first combine the files into a format John the Ripper understands using the `unshadow` tool.

**Syntax**:  
```bash
unshadow [path to passwd] [path to shadow] > [output file]
```

**Example**:  
```bash
unshadow /etc/passwd /etc/shadow > unshadowed.txt
```

**Result**:  
A combined file (`unshadowed.txt`) containing the necessary information for cracking.

#### **Cracking the Password Hash**
Once the `unshadowed.txt` file is created, use John the Ripper to crack the hashes.

**Syntax**:  
```bash
john --wordlist=[path to wordlist] [path to unshadowed file]
```

**If format is required** (e.g., SHA-512 crypt):  
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```

**Example Commands**:  
1. Combine files:  
   ```bash
   unshadow ~/John-the-Ripper-The-Basics/Task06/passwd.txt ~/John-the-Ripper-The-Basics/Task06/shadow.txt > unshadowed.txt
   ```

2. Crack the hash:  
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
   ```

3. View cracked passwords:  
   ```bash
   john --show unshadowed.txt
   ```

#### **Explanation of Commands**
- **`unshadow`**: Merges `/etc/passwd` and `/etc/shadow` files for compatibility with John.  
- **`--wordlist=/usr/share/wordlists/rockyou.txt`**: Specifies the wordlist for the brute-force attack.  
- **`--format=sha512crypt`**: Specifies the hash type if needed.  
- **`john --show`**: Displays cracked passwords.

### **Practical Steps**
1. Navigate to the directory:  
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task06/
   ```

2. Combine `passwd.txt` and `shadow.txt`:  
   ```bash
   unshadow passwd.txt shadow.txt > unshadowed.txt
   ```

3. Crack the hash using John:  
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
   ```

4. View the cracked password:  
   ```bash
   john --show unshadowed.txt
   ```

#### **Analogy**: Cracking `/etc/shadow` Hashes  
Think of `/etc/passwd` and `/etc/shadow` as pieces of a puzzle. The `unshadow` tool combines these pieces to create a full picture, and John the Ripper is the **decoder** that solves the puzzle to reveal the password.  

---
---

### Cracking Passwords with Single Crack Mode in John the Ripper

#### **What is Single Crack Mode?**
- **Single Crack Mode** uses **heuristics and word mangling** to generate possible passwords based on the username or related information.  
- It exploits weak passwords derived from usernames or other user-specific details.

#### **Word Mangling in Action**
Given a username like `Markus`, John might generate:  
- **Number variations**: `Markus1`, `Markus2`, `Markus3`  
- **Case variations**: `MArkus`, `MARkus`, `MARKus`  
- **Special characters**: `Markus!`, `Markus$`, `Markus*`  

#### **Using the GECOS Field**
- **GECOS field** (5th field in `/etc/passwd`): Stores information like the user’s full name or office details.  
- John leverages this information for better word mangling when cracking `/etc/shadow` hashes.

Example `passwd` entry:  
```plaintext
joker:x:1001:1001:Joker:/home/joker:/bin/bash
```
- Here, "Joker" in the GECOS field would be used for mangling.

#### **Syntax for Single Crack Mode**
```bash
john --single --format=[hash format] [path to file]
```

- **`--single`**: Activates Single Crack Mode.  
- **`--format=[hash format]`**: Specifies the hash type (e.g., `raw-sha256`, `md5crypt`).  
- **`[path to file]`**: File containing the hash to crack.  

#### **File Format for Single Crack Mode**
Before using Single Crack Mode, prepend the hash with the username to map it:  
- Original:  
  ```
  1efee03cdcb96d90ad48ccc7b8666033
  ```
- Modified:  
  ```
  joker:1efee03cdcb96d90ad48ccc7b8666033
  ```

#### **Example Commands**
1. **Modify the file**: Add the username before the hash:  
   ```bash
   echo "joker:HASH_HERE" > formatted_hash.txt
   ```

2. **Run Single Crack Mode**:  
   ```bash
   john --single --format=raw-sha256 formatted_hash.txt
   ```

3. **View Results**:  
   ```bash
   john --show formatted_hash.txt
   ```

#### **Practical Steps**
1. **Navigate to the directory**:  
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task07/
   ```

2. **Modify the file**:  
   Edit the file to prepend the username `Joker` to the hash. For example:  
   ```bash
   echo "joker:HASH_FROM_FILE" > joker_hash.txt
   ```

3. **Crack the hash**:  
   Use Single Crack Mode to attempt cracking the hash:  
   ```bash
   john --single --format=raw-sha256 joker_hash.txt
   ```

4. **Check the cracked password**:  
   ```bash
   john --show joker_hash.txt
   ```

#### **Tips**
- Always verify the hash format (e.g., `raw-sha256`, `sha512crypt`).  
- Single Crack Mode works best when usernames or user-related data influence password choices.  

#### **Analogy**:  
Think of Single Crack Mode as **customized guessing**. If wordlist mode is like a general search for passwords, Single Crack Mode is like searching based on clues (e.g., username patterns).  

---
---

### Using Custom Rules in John the Ripper

#### **What are Custom Rules?**
- **Custom Rules** allow you to define specific mangling patterns to dynamically generate passwords that match predictable patterns of password complexity.  
- Useful when you know more about the target's password structure (e.g., patterns with uppercase, numbers, and symbols).

#### **Common Patterns in Password Complexity**
Organizations often enforce password rules like:  
1. **Lowercase letters**  
2. **Uppercase letters**  
3. **Numbers**  
4. **Symbols**

Despite these requirements, **users tend to follow predictable patterns**:  
- Example: `Polopassword1!`  
  - Capital letter at the start.  
  - Number followed by a symbol at the end.  

#### **Custom Rule Syntax**
Custom rules are defined in the `john.conf` file (location varies by installation):  
- Example paths:
  - **TryHackMe AttackBox**: `/opt/john/john.conf`  
  - **Common Linux installs**: `/etc/john/john.conf`  

#### **Creating a Custom Rule**
1. **Define the Rule Name**  
   ```plaintext
   [List.Rules:RuleName]
   ```
   - Replace `RuleName` with a meaningful name for your rule.

2. **Define Modifiers**  
   - **Common Modifiers**:
     - `Az`: Appends characters to the end of the word.  
     - `A0`: Prepends characters to the start of the word.  
     - `c`: Capitalizes characters based on position.  

3. **Define Character Sets**  
   - Use square brackets to specify the range of characters:
     - `[0-9]`: Numbers 0-9.  
     - `[A-Z]`: Uppercase letters.  
     - `[a-z]`: Lowercase letters.  
     - `[!£$%@]`: Specific symbols.  

#### **Example Custom Rule**
To create passwords that match the pattern `Polopassword1!`:
```plaintext
[List.Rules:PoloPassword]
cAz"[0-9] [!£$%@]"
```
- **c**: Capitalizes the first letter.  
- **Az**: Appends a number `[0-9]` and a symbol `[!£$%@]` to the word.  

#### **Using a Custom Rule**
Run John with the custom rule as follows:
```bash
john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]
```

#### **Tips for Writing Custom Rules**
1. **Talk through the pattern**:
   - For example: "Capitalize the first letter, append a number, and then append a symbol."
2. **Test your rules**:
   - Use existing rules (e.g., in `john.conf`) for guidance or debugging.
3. **Explore existing rules**:
   - John comes with an extensive list of pre-built rules. Find them in `john.conf` around **line 678**.

#### **Practical Task**
1. **Navigate to the directory**:
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task08/
   ```

2. **Create your custom rule**:
   - Open the configuration file:
     ```bash
     nano /opt/john/john.conf
     ```
   - Add your custom rule at the end:
     ```plaintext
     [List.Rules:CustomExample]
     cAz"[0-9] [!£$%@]"
     ```

3. **Run John with the custom rule**:
   ```bash
   john --wordlist=[path to wordlist] --rule=CustomExample [path to file]
   ```

4. **Check the results**:
   ```bash
   john --show [path to file]
   ```

#### **Analogy**
Think of Custom Rules as writing a **personalized password generator** for John. Instead of testing every possible password, you're teaching John to prioritize patterns based on what you know about the target's password habits.

---
---

### Cracking Password-Protected Zip Files with John the Ripper

#### **Overview**
John the Ripper can crack password-protected Zip files by first converting the Zip file into a format it can understand using the `zip2john` tool. Once converted, the resulting hash can be cracked using standard techniques.

#### **Step 1: Extracting Hashes with `zip2john`**
The `zip2john` tool generates the hash of the password-protected Zip file in a format John can process.

**Syntax**:
```bash
zip2john [options] [zip file] > [output file]
```

- **[options]**: Specific checksum options (rarely needed).
- **[zip file]**: Path to the Zip file.
- **`>`**: Redirects output to the specified file.
- **[output file]**: The file to store the resulting hash.

**Example**:
```bash
zip2john secure.zip > zip_hash.txt
```
- This command extracts the hash of `secure.zip` and saves it to `zip_hash.txt`.

#### **Step 2: Cracking the Hash with John**
Once the hash is generated, use John to crack it by specifying a wordlist.

**Syntax**:
```bash
john --wordlist=[path to wordlist] [path to hash file]
```

**Example**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```
- This uses the `rockyou.txt` wordlist to attempt cracking the hash in `zip_hash.txt`.

#### **Step 3: Viewing the Cracked Password**
After running John, view the results using:
```bash
john --show [path to hash file]
```

**Example**:
```bash
john --show zip_hash.txt
```
- Displays the cracked password.

#### **Practical Task Instructions**
1. Navigate to the directory containing the Zip file:
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task09/
   ```

2. Generate the hash from the Zip file:
   ```bash
   zip2john secure.zip > zip_hash.txt
   ```

3. Crack the hash using a wordlist:
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
   ```

4. View the cracked password:
   ```bash
   john --show zip_hash.txt
   ```

#### **Key Notes**
- **Wordlist**: Use a comprehensive wordlist like `rockyou.txt` for better results.
- **File Permissions**: Ensure you have the appropriate permissions for the Zip file.
- **Complex Passwords**: For highly complex passwords, consider using a hybrid attack or custom rules.

---
---

### Cracking Password-Protected RAR Archives with John the Ripper

#### **Overview**
John the Ripper can crack password-protected RAR files using a process similar to cracking Zip files. The `rar2john` tool converts the RAR file into a hash format that John can process.

#### **Step 1: Extracting Hashes with `rar2john`**
The `rar2john` tool generates the hash of the RAR file for John.

**Syntax**:
```bash
rar2john [rar file] > [output file]
```

- **[rar file]**: Path to the RAR file.
- **`>`**: Redirects output to the specified file.
- **[output file]**: File to store the resulting hash.

**Example**:
```bash
rar2john secure.rar > rar_hash.txt
```
- This extracts the hash of `secure.rar` and saves it to `rar_hash.txt`.

#### **Step 2: Cracking the Hash with John**
Once the hash is generated, use John to crack it with a wordlist.

**Syntax**:
```bash
john --wordlist=[path to wordlist] [path to hash file]
```

**Example**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
```
- Uses the `rockyou.txt` wordlist to attempt cracking the hash in `rar_hash.txt`.

#### **Step 3: Viewing the Cracked Password**
After running John, view the results using:
```bash
john --show [path to hash file]
```

**Example**:
```bash
john --show rar_hash.txt
```
- Displays the cracked password.

#### **Practical Task Instructions**
1. Navigate to the directory containing the RAR file:
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task10/
   ```

2. Generate the hash from the RAR file:
   ```bash
   rar2john secure.rar > rar_hash.txt
   ```

3. Crack the hash using a wordlist:
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
   ```

4. View the cracked password:
   ```bash
   john --show rar_hash.txt
   ```

#### **Key Notes**
- **RAR Version**: John supports most RAR files but may struggle with RAR5 encryption.
- **Wordlist**: Use a comprehensive wordlist like `rockyou.txt` to improve success rates.
- **Permissions**: Ensure appropriate permissions to access the RAR file.

---
---

### Notes: Cracking SSH Key Passwords with John the Ripper

#### **Overview**
John the Ripper can crack passwords protecting SSH private keys (`id_rsa`). This is often encountered in CTF challenges or when testing password security for private keys.

#### **Step 1: Extracting Hashes with `ssh2john`**
The `ssh2john` (or `ssh2john.py`) tool converts the `id_rsa` file into a hash format compatible with John.

**Syntax**:
```bash
ssh2john [id_rsa file] > [output file]
```

- **[id_rsa file]**: Path to the private key file.
- **`>`**: Redirects the output to a specified file.
- **[output file]**: File where the resulting hash will be saved.

**Example**:
```bash
/opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```
- This extracts the hash of `id_rsa` and saves it to `id_rsa_hash.txt`.

If `ssh2john.py` is not installed, use the path to the script:
- On TryHackMe AttackBox: `/opt/john/ssh2john.py`
- On Kali Linux: `/usr/share/john/ssh2john.py`

**Command Example for AttackBox**:
```bash
python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

#### **Step 2: Cracking the Hash with John**
Once the hash is generated, use John to crack it using a wordlist.

**Syntax**:
```bash
john --wordlist=[path to wordlist] [path to hash file]
```

**Example**:
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```
- Uses the `rockyou.txt` wordlist to attempt cracking the hash in `id_rsa_hash.txt`.

#### **Step 3: Viewing the Cracked Password**
After running John, view the cracked password using:
```bash
john --show [path to hash file]
```

**Example**:
```bash
john --show id_rsa_hash.txt
```

#### **Practical Task Instructions**
1. Navigate to the directory containing the `id_rsa` file:
   ```bash
   cd ~/John-the-Ripper-The-Basics/Task11/
   ```

2. Extract the hash from the `id_rsa` file:
   ```bash
   python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
   ```

3. Crack the hash using a wordlist:
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
   ```

4. View the cracked password:
   ```bash
   john --show id_rsa_hash.txt
   ```

#### **Key Notes**
- **Password Strength**: Cracking depends on the complexity of the password and the wordlist used.
- **Permissions**: Ensure appropriate permissions for accessing the `id_rsa` file.
- **Best Practices**: Use strong, unpredictable passwords for SSH private keys to prevent cracking.

---
---


