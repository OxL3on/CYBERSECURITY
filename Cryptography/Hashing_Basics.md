### Hash Function: Simplified Explanation

**What is a Hash Function?**  
Think of a hash function as a machine that takes input (of any size) and produces a unique "summary" (fixed-size output). Unlike encryption, there’s no key, and you can’t reverse the output to find the original input. 

Key Points:  
- **Fixed Output:** The output size is always the same, no matter how big or small the input is.  
- **Sensitive to Changes:** Even the tiniest change in the input (like flipping one bit) creates a completely different output.  
- **Fast and One-Way:** Hashing is quick but cannot be reversed.  

**Example:**  
Imagine two files:
- **File 1** contains the letter `T` (binary: `01010100`).  
- **File 2** contains the letter `U` (binary: `01010101`).  

Despite differing by just one bit, their MD5, SHA1, or SHA256 hashes will be entirely different.

Commands you can try:  
```bash
md5sum file1.txt file2.txt  
sha1sum file1.txt file2.txt  
sha256sum file1.txt file2.txt  
```

The output will show drastically different hashes for each file, proving how sensitive hash functions are to input changes.

---

**Why is Hashing Important?**  
Hashing is like a cybersecurity superhero! Here’s why:  
1. **Data Integrity:** Ensures data isn’t tampered with.  
2. **Password Protection:** Instead of storing your password, systems store its hash.  
   - Example: When you log into a site like TryHackMe, the server checks if your password's hash matches the stored hash.

---

**Hash Collisions: The Pigeonhole Problem**  
A hash collision happens when two different inputs produce the same hash. While rare, they’re unavoidable because:  
- **Unlimited Inputs vs. Limited Outputs:** Think of a pigeonhole with 21 pigeons (inputs) but only 16 holes (outputs). Some pigeons must share holes!  
- Good hash functions make collisions extremely unlikely.

**Warning:**  
Older algorithms like **MD5** and **SHA1** are now insecure because attackers can intentionally create collisions. Use stronger algorithms like **SHA-256** instead.


---
---

### Password Storage and Data Integrity  

Hashing plays a vital role in two key areas:  
1. **Password Storage** (for authentication).  
2. **Data Integrity** (ensuring data hasn’t been tampered with).  

Here, we focus on **password storage** for authentication systems, not password managers. Authentication only checks if you know the password, so it doesn’t need to store the actual password.  

---

### Stories of Insecure Password Storage  

#### 1. **Plaintext Password Storage**  
Storing passwords in plaintext is highly insecure. If leaked, attackers gain direct access to users' passwords. Since many people reuse passwords across sites, a single leak can compromise multiple accounts.  

**Example:**  
RockYou, a company storing passwords in plaintext, was breached, exposing 14 million passwords. This breach gave birth to the infamous `rockyou.txt` file, widely used in penetration testing today.  

Command to explore the file:  
```bash
wc -l /usr/share/wordlists/rockyou.txt  # Count lines (total passwords)
head /usr/share/wordlists/rockyou.txt  # Preview top passwords
```

---

#### 2. **Using Deprecated Encryption**  
Encryption isn’t suitable for password storage because it can be reversed (decrypted). Adobe’s breach is a classic example. They stored passwords using weak encryption and even stored password hints in plaintext, making it easy to recover passwords.  

---

#### 3. **Using Insecure Hash Functions**  
Hash functions like SHA-1 are considered insecure due to vulnerabilities like hash collisions. LinkedIn’s 2012 breach is a cautionary tale:  
- They used SHA-1 for password hashing.  
- They didn’t use **salting** (adding a random value to the password before hashing).  

Without salting, attackers can use precomputed hash lists (rainbow tables) to crack passwords faster.  

---

**Takeaway:** Always store passwords using strong hashing algorithms (e.g., SHA-256) combined with salting. This ensures better security and protects users from breaches.

---
---


### **Using Hashing to Store Passwords**  

Instead of storing passwords directly, we store their **hash values** using a secure hashing function. This way, even if the database is leaked, attackers must crack each password individually.  

However, there's a problem:  
- **Same Passwords, Same Hash**: If two users have the same password, their hashes will be identical, making it easier for attackers to exploit the data.  
- **Rainbow Tables**: Attackers can use precomputed lookup tables of hashes to quickly reverse common passwords.  

#### **What is a Rainbow Table?**  
A rainbow table is a collection of password-hash pairs, making it faster to find a password from its hash. Here's an example:  

| **Hash**                           | **Password**      |  
|------------------------------------|------------------|  
| `02c75fb22c75b23dc963c7eb91a062cc` | zxcvbnm          |  
| `b0baee9d279d34fa1dfd71aadb908c3f` | 11111            |  
| `e10adc3949ba59abbe56e057f20f883e` | 123456           |  

Websites like **CrackStation** use massive rainbow tables to crack hashes quickly by matching them against their database.  

---

### **Protecting Against Rainbow Tables**  

To protect against rainbow tables, we use **salts**.  
- A **salt** is a random value added to the password before hashing, ensuring that even identical passwords produce different hashes.  
- **Salts are stored in the database alongside the hash** and don't need to be private.  

#### **How Salting Works**  
1. Generate a unique salt for each user (e.g., `Y4UV*^(=go_!`).  
2. Concatenate the password and salt (e.g., `password123 + Y4UV*^(=go_!`).  
3. Hash the combined string.  
4. Store the resulting hash and the salt in the database.  

**Secure Hashing Algorithms like** `Bcrypt`, `Scrypt`, and `Argon2` handle salting automatically.  

---

### **Example of Secure Password Storage**  

Let’s store a password (`AL4RMc10k`) securely:  
1. **Choose a secure hashing algorithm**: Use `Argon2`, `Bcrypt`, or `Scrypt`.  
2. **Generate a salt**: E.g., `Y4UV*^(=go_!`.  
3. **Combine password and salt**: `AL4RMc10kY4UV*^(=go_!`.  
4. **Hash the combined string**.  
5. **Store** the hash and salt in the database.  

---

### **Why Not Encrypt Passwords?**  

Encrypting passwords instead of hashing seems straightforward, but there’s a catch:  
- Encryption requires storing a **decryption key**.  
- If the key is compromised, all passwords can be decrypted instantly.  

This is why hashing is preferred for authentication systems—it’s a one-way process and doesn’t need a key to verify passwords.  

--- 

**Takeaway:** Use secure hashing algorithms with unique salts to ensure robust password protection. Avoid outdated methods like SHA-1 and MD5, and never store passwords in plaintext or rely on encryption for authentication.  

---
---

### Offensive Perspective: Recognizing and Cracking Hashes  

### **Hash Recognition**  

Recognizing a hash type can be challenging, as many hashing algorithms produce visually similar outputs. Automated tools like **hashID** or **Hashcat** can help but may misidentify certain hashes. Use context clues alongside these tools:  
- **Database Source**: A hash from a web application is likely MD5.  
- **Operating System**: A hash from Windows is probably NTLM.  

---

### **Linux Passwords**  

Linux systems store password hashes in the **/etc/shadow** file, accessible only by root. Older systems stored them in the **/etc/passwd** file, readable by all users.  

#### **Structure of the Hash in /etc/shadow**  

Linux password hashes have a specific format:  
```plaintext
$prefix$options$salt$hash
```  

| **Field**     | **Description**                                 |  
|---------------|-------------------------------------------------|  
| `$prefix`     | Algorithm identifier (e.g., `$6$` for SHA-512). |  
| `options`     | Parameters for the hashing algorithm.           |  
| `salt`        | Random value added to the password.             |  
| `hash`        | Final hashed password value.                    |  

#### **Common Linux Prefixes**  
| **Prefix**  | **Algorithm**                            |  
|-------------|------------------------------------------|  
| `$y$`       | **yescrypt** (default, highly secure).   |  
| `$gy$`      | **gost-yescrypt**.                       |  
| `$7$`       | **scrypt** (password-based key derivation). |  
| `$2b$, $2y$`| **bcrypt** (based on Blowfish).          |  
| `$6$`       | **SHA-512**.                             |  
| `$1$`       | **MD5** (md5crypt).                      |  

#### **Example**: Shadow File Entry  
```plaintext
strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::
```  

| **Field** | **Value**                      | **Description**                              |  
|-----------|--------------------------------|----------------------------------------------|  
| Prefix    | `$y$`                          | Algorithm is yescrypt.                       |  
| Options   | `j9T`                          | Parameters for yescrypt.                     |  
| Salt      | `76UzfgEM5PnymhQ7TlJey1`       | Random salt used to ensure uniqueness.       |  
| Hash      | `/OOSg64dhfF.TigVPdzqiFang6uZ` | Final hash value of the salted password.     |  

---

### **Windows Passwords**  

Windows stores password hashes in the **SAM (Security Accounts Manager)** file, which requires special privileges to access.  

#### **Hash Types**  
1. **NT Hashes**: Derived using NTLM (based on MD4).  
2. **LM Hashes**: Older, less secure hashes.  

#### **Tools for Dumping Windows Hashes**  
- **mimikatz**: Extracts hashes from the SAM file.  
- **pwdump**: Dumps hashes from Windows systems.  

#### **Important Note**  
NTLM, MD4, and MD5 hashes look visually similar, so context is essential for determining the correct hash type.

---

### **Cracking Hashes**  

Once the hash type is identified, the next step is to crack it.  

#### **Hashcat**  
A powerful tool for cracking hashes. Supports multiple hash types and offers:  
- **Brute-force attacks**: Tries every possible combination.  
- **Dictionary attacks**: Uses a wordlist (e.g., `rockyou.txt`).  

#### **Rainbow Tables**  
If the hash is unsalted, rainbow tables can quickly match it to a plaintext password.  

#### **Salts Make Cracking Harder**  
If a hash is salted, each password must be cracked individually, making rainbow tables ineffective.

---

### **Resources for Hash Identification and Cracking**  
- **Hashcat Example Hashes**: A comprehensive reference for various hash formats.  
- **CrackStation**: Online hash-cracking tool using rainbow tables.  
- **Linux man pages**: Detailed explanations of hashing algorithms (`man 5 shadow`, `man 5 crypt`).  

---

### **Key Takeaways**  
1. **Recognize the context**: The environment where the hash is found gives clues about its type.  
2. **Use tools wisely**: Automate recognition and cracking, but validate with manual checks.  
3. **Learn prefixes**: Familiarize yourself with Linux-style password prefixes for faster identification.  
4. **Understand limitations**: Salting and strong algorithms significantly increase difficulty for attackers.  

---
---

### **Cracking Passwords with Salt and Tools**  

When dealing with salted hashes, brute-forcing becomes more challenging because the salt makes each password attempt unique.

---

### **Handling Salted Hashes**
- **Salts Prevent Rainbow Tables**: The salt ensures that identical passwords produce different hashes, rendering precomputed rainbow tables ineffective.
- **Cracking Process**:
  1. **Extract the Salt**: Obtain the salt value from the hash format.
  2. **Use the Salt in Cracking Tools**: Pass the salt as an argument in cracking tools like Hashcat or John the Ripper.
  3. **Compare Outputs**: Iterate through password guesses combined with the salt until the hash matches.

---

### **Using GPUs for Cracking**
Modern GPUs are ideal for password cracking due to their ability to perform parallel calculations:
- **Advantages**:
  - Thousands of cores accelerate hash computations.
  - Excellent for unsalted and weaker algorithms like MD5 or NTLM.
- **Limitations**:
  - Hashing algorithms like Bcrypt, scrypt, and Argon2 are designed to resist GPU-based cracking by being computationally expensive.

#### **Running Hashcat with GPU**
To make the most of your GPU:
1. Use Hashcat on the host OS (not a VM).
2. Ensure GPU drivers and OpenCL/CUDA libraries are installed.
3. Example:
   ```bash
   hashcat -m 1000 -a 0 hashfile.txt /usr/share/wordlists/rockyou.txt
   ```
   - `-m 1000`: NTLM hash type.
   - `-a 0`: Straight attack mode.

---

### **Virtual Machines and Cracking**
- **Hashcat on VMs**:
  - GPUs are often inaccessible in VMs unless explicitly configured.
  - Performance is degraded due to virtualisation overhead.
- **John the Ripper**:
  - CPU-based by default, works well in VMs.
  - For better performance, run it on the host OS.

---

### **Practical Example: Cracking with Hashcat**
Let’s say you have the following hash file (`hash.txt`):
```plaintext
$6$salt$hashedpassword
```

Steps to crack:
1. Identify the hash type. Here, `$6$` indicates **SHA-512**.
2. Use the appropriate Hashcat mode for SHA-512 crypt (`-m 1800`).
3. Command:
   ```bash
   hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
   ```

---

### **Hashcat Syntax Breakdown**
- **`-m <hash_type>`**: Numeric code for hash type (e.g., `1000` for NTLM, `1800` for SHA-512 crypt).
- **`-a <attack_mode>`**: Attack strategy:
  - `0`: Straight (wordlist).
  - `1`: Combination (pairs of passwords).
  - `3`: Mask (custom rules).
  - `6`: Hybrid (wordlist + mask).
- **`hashfile`**: File containing the hash.
- **`wordlist`**: Path to the wordlist (e.g., `rockyou.txt`).

---

### **Cracking with John the Ripper**
For hashes like NTLM or MD5:
1. Identify the hash type.
2. Use the command:
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
   ```
3. To resume a stopped session:
   ```bash
   john --restore
   ```

---

### **Best Practices**
- **Start with Rockyou**: The `rockyou.txt` wordlist is comprehensive for testing common passwords.
- **Identify Weak Points**: Look for unsalted hashes or systems using outdated hashing algorithms.
- **Experiment with Tools**: Familiarize yourself with both Hashcat and John the Ripper for diverse cracking scenarios.

---
---

### **Using Hashing for Data Integrity and Authentication**  

#### **Integrity Checking**
Hashing ensures data integrity by verifying that a file or message has not been altered during storage or transmission. This is particularly useful in the following scenarios:

1. **File Downloads**:
   - **Purpose**: Ensure the downloaded file matches the original.
   - **Example**:
     - The Fedora checksum file contains the SHA256 hash of the ISO files.
     - After downloading the ISO, run the `sha256sum` command on the file:
       ```bash
       sha256sum Fedora-Workstation-Live-x86_64-40-1.14.iso
       ```
     - Compare the output with the hash in the checksum file. If they match, the file has not been tampered with.

2. **Duplicate File Detection**:
   - Files with identical hashes are duplicates. This is useful for:
     - Deduplication in storage systems.
     - Identifying redundant backups.

---

#### **HMAC (Keyed-Hash Message Authentication Code)**

HMAC extends the concept of hashing to include **authenticity** alongside **integrity**. It combines a cryptographic hash function with a secret key to achieve the following:
- **Authenticity**: Ensures that the sender of the message is verified.
- **Integrity**: Confirms that the message has not been modified.

##### **How HMAC Works**
1. **Key Padding**:
   - The secret key is padded to the hash function's block size.
2. **Inner Hash**:
   - The padded key is XORed with a constant (called `ipad`).
   - This XORed key is concatenated with the message (`M`) and hashed.
3. **Outer Hash**:
   - The padded key is XORed with another constant (`opad`).
   - This XORed key is concatenated with the result of the inner hash and hashed again.
4. **Final Output**:
   - The result is the fixed-length HMAC value.

##### **Mathematical Representation**
\[
\text{HMAC}(K, M) = H \big( (K \oplus \text{opad}) || H((K \oplus \text{ipad}) || M) \big)
\]
- \( H \): Hash function (e.g., SHA256).
- \( K \): Secret key.
- \( M \): Message.
- \( \oplus \): XOR operation.
- \( \text{ipad} \): Inner padding (usually a block of zeros).
- \( \text{opad} \): Outer padding (usually a block of ones).

---

#### **Applications of HMAC**
1. **API Authentication**:
   - Many APIs use HMAC to authenticate requests. The client generates an HMAC of the request data using a shared secret key, and the server validates it.
2. **Securing Communication**:
   - Ensures the authenticity and integrity of messages in protocols like TLS and IPSec.
3. **Password Storage**:
   - HMAC can strengthen hashed password storage by adding a key.

---

### **Example: Generating an HMAC with Python**
Here’s how to generate an HMAC using the Python `hmac` library:

```python
import hmac
import hashlib

# Message and key
message = b'This is a secure message.'
key = b'supersecretkey'

# Generate HMAC using SHA256
h = hmac.new(key, message, hashlib.sha256)
print(f"HMAC: {h.hexdigest()}")
```

---

### **Key Points**
- **Hashing** checks file integrity but does not verify the source.
- **HMAC** ensures both **authenticity** and **integrity**, making it more robust for sensitive applications.
- Hashing and HMAC are foundational tools in cybersecurity, widely used in secure communications, authentication systems, and data integrity checks.
