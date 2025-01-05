**Introduction to Cryptography**

Cryptography ensures secure communication in the presence of adversaries by protecting data’s confidentiality, integrity, and authenticity.

### Everyday Uses of Cryptography:
1. **Website Logins**: Encrypts your credentials.
2. **SSH Connections**: Creates secure tunnels.
3. **Online Banking**: Ensures safe communication with servers.
4. **File Integrity Checks**: Verifies downloaded files using hashes.

**Key Regulations**:
- **PCI DSS**: Encrypts credit card data.
- **HIPAA/GDPR/DPA**: Protects sensitive personal information.

---

### Basic Concepts:
- **Plaintext**: Original readable message (e.g., "hello").
- **Ciphertext**: Encrypted, unreadable message.
- **Cipher**: Algorithm for encryption and decryption.
- **Key**: Secret bits used by the cipher.
- **Encryption**: Converts plaintext to ciphertext.
- **Decryption**: Converts ciphertext back to plaintext.

#### Example: Caesar Cipher
- **Plaintext**: TRYHACKME
- **Key**: 3 (shift letters right by 3 positions)
- **Ciphertext**: WUBKDFNPH
- To decrypt, shift the letters left by 3.

**Note**: Caesar Cipher is insecure due to vulnerability to brute force attacks (only 25 possible keys).

---

### Types of Encryption

#### 1. **Symmetric Encryption**
- Same key for encryption and decryption.
- **Challenges**: Secure key sharing.

**Common Algorithms**:
- **DES**: 56-bit key; obsolete.
- **3DES**: Repeats DES thrice; deprecated.
- **AES**: Modern standard with 128, 192, or 256-bit keys.

#### 2. **Asymmetric Encryption**
- Public key encrypts; private key decrypts.
- **Advantages**: No private key sharing.
- **Drawbacks**: Slower and uses larger keys.

**Common Algorithms**:
- **RSA**: Key sizes: 2048, 3072, 4096 bits.
- **ECC**: Shorter keys, e.g., 256-bit ECC = 3072-bit RSA security.

---

### Mathematical Operations in Cryptography

#### 1. **XOR Operation**
- Compares two bits: 1 if different, 0 if same.

**Truth Table**:
- 0 ⊕ 0 = 0
- 0 ⊕ 1 = 1
- 1 ⊕ 0 = 1
- 1 ⊕ 1 = 0

**Properties**:
- A ⊕ A = 0
- A ⊕ 0 = A
- Commutative: A ⊕ B = B ⊕ A
- Associative: (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)

**Use in Cryptography**:
- **Encryption**: Ciphertext = Plaintext ⊕ Key.
- **Decryption**: Plaintext = Ciphertext ⊕ Key.

#### 2. **Modulo Operation**
- Finds remainder when one number is divided by another: X % Y.

**Examples**:
- 25 % 5 = 0
- 23 % 6 = 5

Modulo is used in algorithms involving large numbers.

---

### Summary
- **Symmetric Encryption**: Uses the same key (e.g., AES).
- **Asymmetric Encryption**: Uses public/private keys (e.g., RSA, ECC).
- Cryptography relies on XOR and modulo operations for secure algorithms.
- Historical ciphers like Caesar Cipher paved the way for modern cryptography.

**Note**: Cryptography is crucial for secure communication in the digital world!


