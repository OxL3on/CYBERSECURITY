#### 1. **Authentication**:
   - **What It Means**: Verifying the identity of the person you're communicating with.
   - **Example**: In a coffee meeting, you can see and hear your business partner, confirming who they are.
   - **Online**: You need to be sure you're messaging the right person, not an imposter.

#### 2. **Authenticity**:
   - **What It Means**: Ensuring the message is truly coming from the claimed sender.
   - **Example**: You can trust the words your business partner says because you know it's them.
   - **Online**: Verifying that a message hasn't been altered and is from the right person.

#### 3. **Integrity**:
   - **What It Means**: Making sure the message remains unchanged during communication.
   - **Example**: No one can secretly alter your conversation.
   - **Online**: Ensuring the message hasn’t been tampered with as it travels through networks.

#### 4. **Confidentiality**:
   - **What It Means**: Keeping the conversation private and preventing unauthorized access.
   - **Example**: You sit away from others to ensure only your business partner hears you.
   - **Online**: Protecting your message so only the intended recipient can read it.

#### Cryptography Solutions:
   - **Private Key (Symmetric Encryption)**: Protects confidentiality by locking the message so only the receiver can open it.
   - **Public Key (Asymmetric Cryptography)**: Provides authentication, authenticity, and integrity using two keys—public and private.

These concepts—authentication, authenticity, integrity, and confidentiality—are key to secure communication in both the physical and digital worlds. Cryptography ensures these principles are upheld online.

---

### Exchanging Keys with Symmetric and Asymmetric Encryption

#### **Problem: Secure Key Exchange**
- **Challenge**: How do you share a symmetric encryption key securely without it being intercepted by someone snooping?
- **Solution**: Use **asymmetric encryption** to exchange the symmetric key safely.

#### **Analogy: Lock and Box**
- Imagine you have a secret code (symmetric encryption key) and need to send the instructions to your friend without anyone else reading them.
  - You ask your friend for a **lock** (public key).
  - You place the instructions (the symmetric key) in a **box** and lock it with the lock (public key).
  - Only your friend has the **key** (private key) to unlock the box and read the instructions.

#### **Cryptographic System**
- **Secret Code**: Symmetric encryption cipher and key.
- **Lock**: Public key (the server’s public key).
- **Lock’s Key**: Private key (the server’s private key).

#### **How It Works**
1. **Asymmetric encryption** is used once to securely exchange the symmetric key.
2. After exchanging the symmetric key, you can use **symmetric encryption** for fast communication since it’s faster than asymmetric encryption.

#### **Real World Application**
- **Authentication**: To ensure the person you’re communicating with is who they say they are, additional tools like **digital signatures** and **certificates** are used. These will be explored later in the course.

This system lets you exchange keys securely without transmitting them in a way that exposes them to snooping.

---

### RSA Encryption

#### **RSA Overview**
- **RSA** is a public-key encryption algorithm that enables secure data transmission over insecure channels.
- It’s based on the **mathematically difficult problem of factoring large numbers**. Multiplying two large prime numbers is easy, but factoring their product (the reverse process) is computationally hard.
- **Public key**: Used for encryption (shared with everyone).
- **Private key**: Used for decryption (kept secret).

#### **How RSA Works: The Math**
1. **Multiplying Prime Numbers**:
   - Example: 
     - Prime 1: 982451653031
     - Prime 2: 169743212279
     - Their product: 982451653031 × 169743212279 = 166764499494295486767649.
   - Factoring this large number (i.e., finding the original primes) is difficult and takes huge computing power.

2. **RSA Key Generation**:
   - **Choose two prime numbers**: `p` and `q`.
   - **Compute `n = p × q`**: This is used in both the public and private keys.
   - **Calculate `ϕ(n)`**: This is the totient of `n`, which helps in selecting the public and private exponents.
   - **Select `e` (public exponent)**: It should be relatively prime to `ϕ(n)`.
   - **Select `d` (private exponent)**: `e × d ≡ 1 (mod ϕ(n))`.

   **Example:**
   - `p = 157`, `q = 199`
   - `n = 157 × 199 = 31243`
   - `ϕ(n) = 31243 - 157 - 199 + 1 = 30888`
   - Select `e = 163` and `d = 379` such that `e × d = 1 mod ϕ(n)`.

3. **Encrypting and Decrypting Messages**:
   - **Encryption**: 
     - Message `x = 13`, encrypt using the public key `(n, e)`: `y = x^e mod n = 13^163 mod 31243 = 16341`.
   - **Decryption**: 
     - Using the private key `(n, d)`, decrypt the message: `x = y^d mod n = 16341^379 mod 31243 = 13`.

   The encrypted message `y` can only be decrypted by the correct private key `d`.

#### **RSA in Capture The Flag (CTF) Challenges**
- RSA is often featured in **CTF (Capture The Flag)** challenges where you need to break encryption.
- You’re typically given values such as `p`, `q`, `n`, `e`, `d`, `m` (message), and `c` (ciphertext).
  
  **Variables**:
  - `p` and `q`: Large prime numbers.
  - `n`: Product of `p` and `q` (part of both keys).
  - `e`: Public exponent.
  - `d`: Private exponent.
  - `m`: Original message (plaintext).
  - `c`: Encrypted message (ciphertext).

- **Example CTF Tools**:
  - **RsaCtfTool**: A popular tool for solving RSA challenges.
  - **rsatool**: Another tool for working with RSA encryption.

- **Goal**: In CTFs, you’ll often be given these variables and need to **decrypt a message** or **break the encryption** to retrieve the flag.

#### **Summary**
RSA encryption uses the difficulty of factoring large numbers to secure communication. It relies on two keys: a public key for encryption and a private key for decryption. While the math behind RSA is complex, understanding the core concepts (prime numbers, modular arithmetic, and key generation) is essential for both real-world applications and solving RSA challenges in CTFs.


---

### Diffie-Hellman Key Exchange

#### **Problem: Sharing a Secret Key Securely**
- **Challenge**: You want to send a password-protected document to your business partner, but you need a secure way to share the password (the secret key) without anyone else intercepting or altering it.
- **Solution**: Use **Diffie-Hellman Key Exchange** to establish a shared secret over an insecure channel.

#### **What is Diffie-Hellman Key Exchange?**
- It is a method that allows two parties (e.g., Alice and Bob) to **agree on a shared secret key** for symmetric encryption without directly transmitting the key over the insecure channel.
- The beauty of Diffie-Hellman is that even if someone is eavesdropping on the communication, they cannot easily figure out the shared secret key.

#### **How Does It Work?**
1. **Public Agreement**:
   - Alice and Bob agree on two public values: 
     - A large prime number `p`.
     - A generator `g` (a value between 0 and `p`).
   - These values are sent openly over the insecure channel. For simplicity, we use small numbers in the example: `p = 29`, `g = 3`.

2. **Private Keys**:
   - Alice and Bob each choose a **private integer** (secret key):
     - Alice chooses `a = 13`.
     - Bob chooses `b = 15`.
   - These private keys must remain secret.

3. **Generate Public Keys**:
   - Alice and Bob calculate their **public keys** based on their private keys and the agreed-upon values:
     - Alice calculates: `A = g^a mod p = 3^13 mod 29 = 19`.
     - Bob calculates: `B = g^b mod p = 3^15 mod 29 = 26`.
   - These public keys are sent to each other.

4. **Key Exchange**:
   - Alice receives Bob’s public key `B = 26`.
   - Bob receives Alice’s public key `A = 19`.

5. **Calculate the Shared Secret**:
   - Now, both Alice and Bob can calculate the shared secret:
     - Alice calculates: `B^a mod p = 26^13 mod 29 = 10`.
     - Bob calculates: `A^b mod p = 19^15 mod 29 = 10`.
   - Both calculations give the same result, `10`, which is the **shared secret key**.

#### **Real-World Application**
- In real-world use, much larger values for `p` and `g` are chosen to ensure security.
- Diffie-Hellman is often combined with **RSA encryption** for a comprehensive security solution:
  - **Diffie-Hellman** is used for establishing the shared key.
  - **RSA** is used for encryption, authentication, and digital signatures.

#### **Benefits of Diffie-Hellman**
- **Secure Key Agreement**: Allows two parties to establish a shared key without ever sending it over the channel.
- **Prevents Eavesdropping**: Even if an attacker intercepts the communication, they cannot easily calculate the shared secret key.

#### **Summary**
Diffie-Hellman enables secure key exchange over an insecure channel by using mathematical principles that allow two parties to independently generate the same shared secret key. This shared key can then be used for **symmetric encryption** in subsequent communications, ensuring confidentiality and security.

---

### SSH Authentication

#### **1. Authenticating the Server**
- When you connect to an SSH server, the client verifies the server's identity by checking its **public key fingerprint**.
- **Example**: 
  - If the SSH client doesn’t recognize the server's public key, it asks for confirmation:
    ```
    The authenticity of host '10.10.244.173' can't be established.
    ED25519 key fingerprint is SHA256:lLzhZc7YzRBDchm02qTX0qsLqeeiTCJg5ipOT0E/YM8.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    ```
- **Reason for Confirmation**: This is a security measure to prevent **man-in-the-middle (MITM) attacks**, where a malicious server could impersonate the target server.
- Once you confirm, the SSH client will record the server's public key for future connections.

#### **2. Authenticating the Client**
- After authenticating the server, the client needs to authenticate itself (prove its identity).
- **Traditional Authentication**: SSH can use **username/password** for authentication, but this is not considered secure.
- **Better Practice**: SSH **key-based authentication** (using **public** and **private keys**).
  
  **SSH Key Types**:
  - **RSA**: Common key type (default).
  - **Ed25519**: Modern, more secure, and recommended key type.
  - **Other Options**: DSA, ECDSA, ECDSA-SK, Ed25519-SK.
  
- **Generating SSH Key Pair**:
  - Use `ssh-keygen` to generate a public/private key pair.
  - Command: `ssh-keygen -t ed25519` (Ed25519 is recommended).
  - **Example Output**:
    ```
    Your identification has been saved in /home/user/.ssh/id_ed25519
    Your public key has been saved in /home/user/.ssh/id_ed25519.pub
    ```
  - **Private Key**: The private key stays with you and should be protected (use a passphrase for extra security).
  - **Public Key**: This is shared with the server (added to the `authorized_keys` file on the server).

#### **3. SSH Private Keys**
- **Private Key**: Never share your private key. If someone has it, they can access systems that trust your public key.
- **Passphrase**: You can encrypt your private key with a passphrase for added security. The passphrase only decrypts the private key on your local system; it’s never transmitted over the network.
- **Key Permissions**: Ensure that private key permissions are strict:
  - Only the owner should be able to read/write (chmod 600).

#### **4. Using SSH Keys for Authentication**
- To use an SSH key, copy your **public key** to the remote server (typically to the `~/.ssh/authorized_keys` file).
  - Command: `ssh-copy-id user@host`.
- **Better Shell with SSH Keys**:
  - During penetration testing or CTFs, SSH keys can be used to **"upgrade" a reverse shell** (from a less stable shell to a more reliable one).
  - Leave an SSH key in the `authorized_keys` file as a **backdoor**.
  - This avoids issues like **unstable reverse shells** (e.g., loss of tab completion or inability to exit properly).

#### **5. Keys Trusted by the Remote Host**
- The remote host stores trusted keys in the `~/.ssh/authorized_keys` file.
- By default, many systems use **key-based authentication** instead of passwords for added security.
  - **Important**: For secure access, only **key authentication** should be allowed (no password-based access).

#### **Conclusion**
SSH key authentication is more secure than password-based authentication and is the best practice for securing SSH access. Always protect your private key and use strong passphrases when generating SSH keys. Additionally, SSH keys are useful in CTFs and penetration testing to ensure reliable access, as they can be used to establish persistent access or "backdoors" in a system.

---

### Digital Signatures and Certificates

#### **1. Digital Signature**
- A **digital signature** verifies the authenticity and integrity of a digital document or message, much like signing a paper document in the physical world.
- **How It Works**:
  - You use your **private key** to create the signature.
  - The recipient uses your **public key** to verify the signature.
  - The process ensures:
    - **Authenticity**: Verifies who created or modified the document.
    - **Integrity**: Ensures the document hasn’t been altered since it was signed.

- **Steps for Digital Signature**:
  - **Create a Hash**: The document is hashed (using a hashing algorithm like SHA-256) to create a unique fingerprint.
  - **Encrypt the Hash**: The hash is then encrypted with your **private key** to create the digital signature.
  - **Verification**: The recipient decrypts the signature using your **public key** and compares it with their own hash of the document. If they match, the document is authentic and hasn’t been altered.

- **Digital vs. Electronic Signatures**:
  - A **digital signature** is based on cryptographic techniques (private/public key pair) and proves the document’s integrity.
  - An **electronic signature** is just an image or scanned version of a physical signature and doesn’t guarantee the document’s integrity.

#### **2. Certificates**
- **Certificates** are used to prove the identity of websites and individuals, often in combination with **public key cryptography**.
  - They ensure you are communicating with the real entity, e.g., confirming that a website is really "tryhackme.com".
  
- **How Certificates Work**:
  - **Public Key Infrastructure (PKI)**: Certificates are issued by a trusted entity known as a **Certificate Authority (CA)**.
  - **Chain of Trust**:
    - Your browser or device trusts a set of **root CAs** by default.
    - When a server presents a certificate, the browser checks if it was issued by a trusted CA in the chain.
    - If the certificate is valid and the CA is trusted, your browser considers the connection secure (e.g., HTTPS).

- **Example**: When you visit a website with HTTPS:
  1. The web server sends its certificate (signed by a trusted CA).
  2. Your browser verifies the certificate against the list of trusted root CAs.
  3. If verified, the connection is secured using **TLS/SSL** encryption.

- **Obtaining a Certificate**:
  - You can get a **TLS certificate** for your website from a CA (e.g., for a fee).
  - Alternatively, **Let's Encrypt** offers free certificates for domains you own.

#### **3. Importance of Digital Signatures and Certificates**
- **Digital Signatures**:
  - Ensure document authenticity and integrity, widely used in legal, financial, and software distribution contexts.
- **Certificates**:
  - Secure online communication by ensuring that websites are trustworthy, especially when using HTTPS to encrypt data.

### Conclusion
Digital signatures use cryptography to verify a document’s authenticity and integrity, while certificates provide a way to prove identities and establish trust online. Both play vital roles in securing digital communication and ensuring that interactions on the internet are legitimate and secure.

---

### GPG (Pretty Good Privacy)

#### **1. What is GPG?**
- **GPG (GnuPG)** is an open-source encryption tool based on the **OpenPGP** standard, widely used for encrypting files, signing messages, and securing emails.
- GPG allows users to:
  - Encrypt messages to keep them confidential.
  - Sign messages to confirm the sender's identity and integrity.
  
#### **2. How GPG Works:**
- GPG uses **public key cryptography**. Each user has two keys:
  - **Public Key**: Used to encrypt messages that only the holder of the private key can decrypt.
  - **Private Key**: Used to decrypt messages and sign documents, proving your identity.

#### **3. Generating a GPG Key Pair:**
- To create a GPG key pair, you use the command `gpg --full-gen-key`, which prompts you through several steps:
  1. **Select Key Type**: Choose between different cryptographic algorithms.
     - **RSA and RSA**: Common choice for signing and encryption.
     - **ECC (Elliptic Curve Cryptography)**: A more modern and efficient choice (e.g., Curve 25519).
  2. **Set Expiry Date**: Decide how long your key will be valid.
  3. **Enter User Information**: Provide your name, email address, and a comment (optional) to identify the key.
  
Example of GPG generation process:

```bash
gpg --full-gen-key
Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (9) ECC (sign and encrypt) *default*
...
Real name: strategos
Email address: strategos@tryhackme.thm
...
```

#### **4. Key Usage in Communication:**
- **Encrypting and Signing**:
  - **Public Key**: Share your public key with others. When they want to send you a secure message, they will encrypt it with your public key.
  - **Private Key**: Use your private key to decrypt messages sent to you and verify signatures.

- **Decrypting Messages**: After importing your private key (e.g., from a backup), you can decrypt messages with:
  ```bash
  gpg --decrypt confidential_message.gpg
  ```

#### **5. Backing Up and Importing Keys:**
- It’s important to keep a secure backup of your private key because it’s used for decryption and signing. If you switch computers, you can import the key using:
  ```bash
  gpg --import backup.key
  ```

#### **6. Protecting Your Private Key with a Passphrase**:
- Similar to SSH keys, **GPG private keys** can be encrypted with a **passphrase** to prevent unauthorized access.
- If the private key is protected by a passphrase, you can use **John the Ripper** to attempt cracking the passphrase.

#### **7. Practical Use in CTFs and Penetration Testing**:
- In **Capture The Flag (CTF)** challenges and **pen testing** exercises, GPG might be used to encrypt/decrypt flags or other important files.
- If you encounter encrypted files, you’ll need your private key to decrypt them, using commands like `gpg --decrypt`.

#### **8. Digital Signatures in GPG**:
- GPG can also be used to sign files or emails, providing proof of the origin of the document and confirming it hasn’t been altered.

### Summary:
- **GPG** is a tool for **signing** and **encrypting** messages and files using public key cryptography.
- It ensures **confidentiality** (only the intended recipient can decrypt) and **authenticity** (the sender can be verified).
- It’s widely used for secure email communication, file encryption, and digital signatures. 
- Always ensure to **backup** your private key and use a **strong passphrase** for protection.

---

