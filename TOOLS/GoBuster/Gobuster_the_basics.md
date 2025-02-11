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


### **Gobuster: Subdomain Enumeration**


#### **What is Subdomain Enumeration?**
- **Subdomain Enumeration** is the process of discovering subdomains (e.g., `www`, `shop`, `api`) of a target domain.
- Subdomains often host different services or applications, which may have unique vulnerabilities not present in the main domain.


#### **Why Use Gobuster's `dns` Mode?**
- To find hidden subdomains that might expose:
  - Admin panels (`admin.example.com`)
  - Testing environments (`dev.example.com`)
  - Backup servers (`backup.example.com`)
- Helps identify potential attack surfaces during penetration testing.


#### **Basic Command Structure**
```bash
gobuster dns -d example.thm -w /path/to/wordlist [flags]
```
- `dns`: Enables DNS subdomain enumeration mode.
- `-d`: Specifies the target domain (e.g., `example.thm`).
- `-w`: Path to the wordlist file containing subdomain guesses.
- `[flags]`: Additional options to customize the scan.


#### **Key Flags for `dns` Mode**
| Flag       | Long Flag          | Description                                                                 |
|------------|--------------------|-----------------------------------------------------------------------------|
| `-c`       | `--show-cname`     | Shows CNAME records (aliases) for subdomains. Cannot be used with `-i`.    |
| `-i`       | `--show-ips`       | Displays IP addresses that subdomains resolve to.                          |
| `-r`       | `--resolver`       | Specifies a custom DNS server to use for resolving queries.                |


#### **Example 1: Basic Subdomain Enumeration**
Command:
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
- Scans for subdomains of `example.thm`.
- Uses the `subdomains-top1million-5000.txt` wordlist.

How it works:
- Gobuster takes each word from the wordlist (e.g., `www`, `shop`) and appends it to the domain (e.g., `www.example.thm`).
- It performs a DNS query to check if the subdomain exists.

Sample Output:
```
Found: www.example.thm
Found: shop.example.thm
Found: academy.example.thm
Found: primary.example.thm
```

#### **Example 2: Show Resolved IPs**
Command:
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -i
```
- Adds the `-i` flag to display the IP addresses of resolved subdomains.

Sample Output:
```
Found: www.example.thm [192.168.1.10]
Found: shop.example.thm [192.168.1.11]
Found: academy.example.thm [192.168.1.12]
```

#### **Example 3: Use a Custom DNS Resolver**
Command:
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -r 8.8.8.8
```
- Adds the `-r` flag to use Google's DNS server (`8.8.8.8`) for resolving queries.


#### **Tips for Success**
1. **Use a Comprehensive Wordlist**: Use large wordlists like `subdomains-top1million-5000.txt` for thorough scanning.
2. **Check Resolved IPs**: Use `-i` to identify where subdomains are hosted.
3. **Custom DNS Servers**: Use `-r` if the default DNS resolver is slow or unreliable.
4. **Save Results**: Redirect output to a file for later analysis:
   ```bash
   gobuster dns -d example.thm -w /path/to/wordlist > results.txt
   ```

#### **-----**
Imagine Gobuster as a **treasure map explorer**:
- The main domain (`example.thm`) is the starting point.
- Each subdomain (`www`, `shop`, `academy`) is a hidden island.
- Gobuster uses a **map (wordlist)** to search for islands by checking their coordinates (DNS queries).
- When it finds an island, it marks it down (`Found: shop.example.thm`).


#### **Key Takeaways**
1. **Wordlists Matter**: Use high-quality wordlists like `subdomains-top1million-5000.txt`.
2. **Show IPs**: Use `-i` to see where subdomains are hosted.
3. **Custom Resolvers**: Use `-r` for faster or more reliable DNS queries.
4. **CNAME Records**: Use `-c` to discover aliases for subdomains.

---
---


### **Gobuster: Vhost Enumeration**


#### **What is Vhost Enumeration?**
- **Vhost (Virtual Host) Enumeration** is the process of discovering virtual hosts running on the same server.
- Virtual hosts allow multiple websites to share the same IP address but appear as separate domains or subdomains.


#### **Why Use Gobuster's `vhost` Mode?**
- To find hidden or misconfigured virtual hosts that might expose:
  - Internal tools (`admin.example.com`)
  - Testing environments (`dev.example.com`)
  - Backup servers (`backup.example.com`)
- Helps identify potential attack surfaces during penetration testing.

#### **Basic Command Structure**
```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist [flags]
```
- `vhost`: Enables virtual host enumeration mode.
- `-u`: Specifies the base URL (e.g., `http://example.thm`).
- `-w`: Path to the wordlist file containing subdomain guesses.
- `[flags]`: Additional options to customize the scan.


#### **Key Flags for `vhost` Mode**
| Short Flag | Long Flag          | Description                                                                 |
|------------|--------------------|-----------------------------------------------------------------------------|
| `-u`       | `--url`            | Specifies the target URL (e.g., `http://example.thm`).                     |
| `--append-domain` |             | Appends the base domain to each word in the wordlist (e.g., `blog.example.com`). |
| `--domain` |                    | Sets the top-level and second-level domain (e.g., `example.thm`).          |
| `--exclude-length` |           | Filters out responses based on their body size to reduce false positives.  |
| `-r`       | `--follow-redirect`| Follows HTTP redirects (useful if subdomains redirect).                    |


#### **Example 1: Basic Vhost Enumeration**
Command:
```bash
gobuster vhost -u "http://10.10.226.147" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```
- Scans for virtual hosts on `10.10.226.147`.
- Uses the `subdomains-top1million-5000.txt` wordlist.
- Appends `example.thm` to each word in the wordlist (e.g., `www.example.thm`, `shop.example.thm`).

Sample Output:
```
Found: blog.example.thm Status: 200 [Size: 1493]
Found: shop.example.thm Status: 200 [Size: 2983]
Found: www.example.thm Status: 200 [Size: 84352]
```

#### **Example 2: Exclude False Positives**
Command:
```bash
gobuster vhost -u "http://10.10.226.147" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```
- Adds `--exclude-length 250-320` to filter out responses with body sizes between 250 and 320 bytes (common for false positives).

Sample Output:
```
Found: blog.example.thm Status: 200 [Size: 1493]
Found: shop.example.thm Status: 200 [Size: 2983]
```

#### **How It Works**
1. Gobuster sends HTTP requests with different `Host` headers.
   - Example Request:
     ```
     GET / HTTP/1.1
     Host: www.example.thm
     User-Agent: gobuster/3.6
     ```
2. The server responds based on the `Host` header.
3. Gobuster checks the response status code and body size to determine valid virtual hosts.


#### **Tips for Success**
1. **Use a Comprehensive Wordlist**: Use large wordlists like `subdomains-top1million-5000.txt`.
2. **Filter False Positives**: Use `--exclude-length` to remove common false positives.
3. **Append Domain**: Always use `--append-domain` to ensure proper hostname formatting.
4. **Follow Redirects**: Use `--follow-redirect` if subdomains may redirect.


#### **-----**
Imagine Gobuster as a **detective searching for secret identities**:
- The server (`10.10.226.147`) is hosting multiple websites, each with its own identity (virtual host).
- Gobuster uses a **list of names (wordlist)** to guess each website’s identity by changing the `Host` header in its requests.
- When it finds a match (e.g., `blog.example.thm`), it reports it back.


#### **Key Takeaways**
1. **Wordlists Matter**: Use high-quality wordlists like `subdomains-top1million-5000.txt`.
2. **Filter Responses**: Use `--exclude-length` to reduce false positives.
3. **Append Domain**: Always use `--append-domain` for proper hostname formatting.
4. **Understand the Difference**: Vhosts are IP-based, while subdomains are DNS-based.

