### **Gobuster: Introduction**

#### **What is Gobuster?**
- **Gobuster** is a tool used to find hidden resources like directories, files, subdomains, and cloud storage buckets.
- It works by **brute-forcing** (trying many possibilities) using wordlists and analyzing responses.
- Used in **penetration testing**, **bug bounty hunting**, and **cybersecurity assessments**.
#### **Key Concepts**
1. **Enumeration**: Listing all available resources (e.g., directories, subdomains).
2. **Brute Force**: Trying every possibility until a match is found (like trying 10 keys on a lock).


#### **Modes of Gobuster**
Gobuster has multiple modes for different tasks:
| Mode    | Purpose                                      |
|---------|----------------------------------------------|
| `dir`   | Enumerates directories and files on a web server. |
| `dns`   | Finds DNS subdomains.                        |
| `vhost` | Enumerates virtual hosts (VHOSTs).           |
| `s3`    | Discovers Amazon AWS S3 buckets.             |
| `gcs`   | Discovers Google Cloud Storage buckets.      |


#### **Basic Command Structure**
```bash
gobuster [mode] -u [target URL] -w [wordlist] [flags]
```
- `[mode]`: The type of scan (e.g., `dir`, `dns`, `vhost`).
- `-u`: The target URL or domain.
- `-w`: Path to the wordlist file.
- `[flags]`: Additional options like threads, delay, etc.


#### **Common Flags**
| Short Flag | Long Flag       | Description                                                                 |
|------------|-----------------|-----------------------------------------------------------------------------|
| `-t`       | `--threads`     | Number of threads (default: 10). Increase for faster scans (e.g., `-t 64`). |
| `-w`       | `--wordlist`    | Specifies the wordlist file to use.                                         |
| `--delay`  |                 | Adds a delay between requests to avoid detection.                           |
| `--debug`  |                 | Enables debug mode for troubleshooting.                                     |
| `-o`       | `--output`      | Saves results to a file (e.g., `-o output.txt`).                            |
| `-q`       | `--quiet`       | Suppresses unnecessary output (e.g., banner, progress).                     |


#### **Example: Directory Enumeration**
Command:
```bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```
- `dir`: Scans for directories and files.
- `-u "http://www.example.thm/"`: Targets the website.
- `-w /usr/share/wordlists/dirb/small.txt`: Uses the `small.txt` wordlist.
- `-t 64`: Runs 64 threads for faster scanning.

How it works:
- Gobuster takes each word from the wordlist (e.g., `images`) and appends it to the URL (`http://example.thm/images/`).
- It sends a request and checks if the resource exists.


#### **-----**
Imagine Gobuster as a **treasure hunter**:
- You give it a map (`wordlist`) and a location (`URL`).
- It tries every spot on the map to find hidden treasures (directories, files, or subdomains).
- If it finds something, it marks it on the map (`output file`).

#### **Key Takeaways**
1. **Wordlists Matter**: Use good wordlists (e.g., `/usr/share/wordlists/dirb/common.txt`) for better results.
2. **Threads Speed Things Up**: Increase threads (`-t`) but don’t overload the system.
3. **Avoid Detection**: Add delays (`--delay`) to mimic normal traffic.
4. **Save Results**: Always save output to a file (`-o`) for later analysis.

---
---


### **Gobuster: Directory and File Enumeration**


#### **What is Directory/File Enumeration?**
- **Directory/File Enumeration** is the process of discovering hidden directories and files on a web server.
- Websites often follow predictable directory structures (e.g., `/admin`, `/images`, `/wp-content`), making them vulnerable to brute force attacks using wordlists.


#### **Why Use Gobuster's `dir` Mode?**
- To uncover hidden resources like:
  - Admin panels (`/admin`)
  - Configuration files (`config.php`)
  - Backup files (`backup.zip`)
- Helps map out the structure of a website for further analysis during penetration testing.


#### **Basic Command Structure**
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist [flags]
```
- `dir`: Enables directory/file enumeration mode.
- `-u`: Specifies the target URL (must include the protocol: `http://` or `https://`).
- `-w`: Path to the wordlist file.
- `[flags]`: Additional options to customize the scan.


#### **Key Flags for `dir` Mode**
| Flag       | Long Flag               | Description                                                                 |
|------------|-------------------------|-----------------------------------------------------------------------------|
| `-x`       | `--extensions`          | Specify file extensions to search for (e.g., `.php`, `.js`).                |
| `-r`       | `--followredirect`      | Follow redirects (e.g., status code 301 or 302).                            |
| `-s`       | `--status-codes`        | Show only specific HTTP status codes (e.g., `200`, `301`, `403`).           |
| `-b`       | `--status-codes-blacklist` | Exclude specific HTTP status codes from results.                         |
| `-k`       | `--no-tls-validation`   | Skip SSL/TLS certificate validation (useful for self-signed certificates).  |
| `-n`       | `--no-status`           | Hide status codes in the output (keeps the screen clean).                   |
| `-c`       | `--cookies`             | Add cookies (e.g., session IDs) to each request.                           |
| `-H`       | `--headers`             | Add custom headers to requests.                                            |
| `-U`/`-P`  | `--username`/`--password` | Authenticate with credentials (if required).                              |


#### **Example 1: Basic Directory Enumeration**
Command:
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
- Scans the root directory (`/`) of `http://www.example.thm`.
- Uses the `directory-list-2.3-medium.txt` wordlist.
- Follows redirects (`-r`).

How it works:
- Gobuster appends each word from the wordlist to the base URL (e.g., `http://www.example.thm/admin`).
- It sends a request and checks the response (e.g., status code `200` = success, `403` = forbidden).

#### **Example 2: Searching for Specific File Types**
Command:
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js
```
- Looks for `.php` and `.js` files in addition to directories.
- Example: If the wordlist contains `login`, Gobuster will check:
  - `http://www.example.thm/login`
  - `http://www.example.thm/login.php`
  - `http://www.example.thm/login.js`

#### **Example 3: Filtering by Status Codes**
Command:
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -s 200,301
```
- Only shows results with status codes `200` (OK) or `301` (Redirect).

#### **Tips for Success**
1. **Use the Right Wordlist**: Choose wordlists based on the target (e.g., `directory-list-2.3-medium.txt` for general use, `wordpress.txt` for WordPress sites).
2. **Recursive Scanning**: Gobuster doesn’t scan recursively. If you find a directory like `/admin`, run another scan targeting `/admin`:
   ```bash
   gobuster dir -u "http://www.example.thm/admin" -w /path/to/wordlist
   ```
3. **Avoid Detection**: Use delays (`--delay`) or reduce threads (`-t`) to mimic normal traffic.
4. **Save Results**: Use `-o` to save output to a file:
   ```bash
   gobuster dir -u "http://www.example.thm" -w /path/to/wordlist -o results.txt
   ```

#### **-----**
Imagine Gobuster as a **detective searching for secret rooms** in a mansion:
- The mansion is the **website**, and each room is a **directory** or **file**.
- The detective uses a **map (wordlist)** to try every door (URL).
- When a door opens (`status code 200`), the detective notes it down.
- If the door is locked (`status code 403`), the detective skips it.

#### **Key Takeaways**
1. **Wordlists Matter**: Use appropriate wordlists for better results.
2. **Filter Results**: Use `-s` or `-b` to focus on relevant status codes.
3. **Extensions Help**: Use `-x` to search for specific file types (e.g., `.php`, `.js`).
4. **Follow Redirects**: Use `-r` to explore redirected paths.
5. **Recursive Scanning**: Manually scan subdirectories if needed.

---
---


