### Domain Name System (DNS)


#### **What is DNS?**
- **DNS (Domain Name System)** is a hierarchical system that maps **domain names** (like www.example.com) to **IP addresses** (like 93.184.215.14), making it easier for users to access websites and services by name instead of remembering numeric IP addresses.


#### **DNS and the OSI Model**
- DNS operates at the **Application Layer** (Layer 7) of the **ISO OSI model**.


#### **DNS Ports**
- **UDP port 53**: The default port used for DNS queries.
- **TCP port 53**: Used for DNS queries that require more reliability or when the response data exceeds 512 bytes.


#### **Common DNS Records**
1. **A Record**:
   - Maps a **hostname** to one or more **IPv4 addresses**.
   - Example: `example.com` → `172.17.2.172`.

2. **AAAA Record**:
   - Similar to the A Record but maps a **hostname** to **IPv6 addresses**.
   - Example: `example.com` → `2606:2800:21f:cb07:6820:80da:af6b:8b2c`.

3. **CNAME Record**:
   - Maps a **domain name** to another **domain name**.
   - Example: `www.example.com` → `example.com`.

4. **MX Record**:
   - Specifies the **mail server** responsible for handling emails for a domain.
   - Example: `mail.example.com` handles emails for `example.com`.


#### **DNS Query and Response Process**
When you type a domain (e.g., `example.com`) in your browser, the browser performs the following steps:
1. **Query**: The browser queries a **DNS server** for the **A record** (to find the IPv4 address).
2. **Response**: The DNS server responds with the corresponding **IP address**.


#### **Example with `nslookup`**
- **Command**: `nslookup www.example.com`
- **Output**:
  - **IPv4 Address**: `93.184.215.14`
  - **IPv6 Address**: `2606:2800:21f:cb07:6820:80da:af6b:8b2c`

**Explanation**:
- `nslookup` queries the DNS for both **A** and **AAAA** records of `www.example.com` and returns the respective addresses.


#### **DNS Query Process with `tshark`**
In this scenario, **`tshark`** is used to capture DNS packets and examine the query/response process. Here’s an example:

1. **DNS Query** for A Record:
   - `Standard query 0x2e0f A www.example.com`
   - **Response**: A record returned `93.184.215.14`.

2. **DNS Query** for AAAA Record:
   - `Standard query 0x96e1 AAAA www.example.com`
   - **Response**: AAAA record returned `2606:2800:21f:cb07:6820:80da:af6b:8b2c`.


#### **Summary**
- **DNS** translates human-readable domain names into machine-readable IP addresses.
- Key **DNS records** include **A**, **AAAA**, **CNAME**, and **MX**.
- **DNS traffic** usually uses **UDP port 53**, but **TCP port 53** is used in certain cases (e.g., larger responses).
- You can use tools like `nslookup` to manually query DNS records.


---
---


### WHOIS


#### **Domain Registration**
- When you register a domain name (e.g., `example.com`), you are granted **authority** to set various **DNS records** (like A, AAAA, and MX records) for that domain.
- **Annual Fee**: Domain names need to be renewed every year, and you must pay an annual fee to keep the domain registered.
- **Contact Information**: You are required to provide accurate contact information, such as your name, phone number, email, and physical address.
  

#### **WHOIS Records**
- **WHOIS** is a service that allows anyone to look up **registration details** of a domain.
- **WHOIS Record** contains:
  1. **Registrant Information**: Name, address, phone, email of the domain owner.
  2. **Domain Registration Details**: Information about when the domain was created, last updated, and when it will expire.
  3. **Registrar Information**: The company through which the domain was registered (e.g., GoDaddy).
  

#### **Privacy Protection**
- Many domain owners use **privacy protection services** to **hide their personal information** in WHOIS records. This helps protect privacy by showing **generic information** (e.g., "DomainsByProxy.com") instead of the actual registrant's contact details.

---

#### **WHOIS Lookup Example**
- To perform a WHOIS lookup, you can use the **`whois` command** (available on Linux, macOS, and some Windows environments).
  
**Example WHOIS Lookup Command**:
```bash
whois example.com
```

- In cases where privacy protection is used, the WHOIS record may show information like:
  ```bash
  Registrant Name: Registration Private
  Registrant Organization: Domains By Proxy, LLC
  Registrant Street: DomainsByProxy.com
  ```


#### **Summary**
- **Domain registration** gives you the authority to set DNS records for your domain.
- **WHOIS records** provide public information about the registrant, including personal details, registration date, and registrar.
- You can use **privacy protection services** to hide personal information from the public WHOIS records.

---
---


### HTTP(S): Accessing the Web


#### **HTTP and HTTPS Overview**
- **HTTP**: Hypertext Transfer Protocol, used for transferring data between a web browser and a web server.
- **HTTPS**: HTTP Secure, the secure version of HTTP, which uses SSL/TLS encryption for privacy and security.
- **Common Ports**: 
  - **HTTP** uses **TCP port 80**.
  - **HTTPS** uses **TCP port 443**.
  - Sometimes **8080** or **8443** are used for alternative HTTP/HTTPS traffic.


#### **Common HTTP Methods**
1. **GET**: Retrieves data (e.g., HTML, images) from the server.
2. **POST**: Submits data to the server (e.g., form submissions, file uploads).
3. **PUT**: Creates or updates resources on the server.
4. **DELETE**: Deletes a specified resource from the server.


#### **Browser-Server Communication**
- **Behind the scenes**: When you access a website, your browser sends HTTP/HTTPS requests to the server.
- **Using Wireshark**: You can capture and examine the packets exchanged between the browser and server, such as HTTP headers, server information, page metadata, etc.
- **Example**: A request to retrieve a webpage may include data such as the HTTP method, the resource path, and headers like `Host` to specify the domain.


#### **Example: Using Telnet to Troubleshoot**
- **Telnet** can be used to manually send HTTP requests to a server:
  - For the home page: 
    ```bash
    GET / HTTP/1.1
    Host: <server>
    ```
  - For a specific file (e.g., `file.html`):
    ```bash
    GET /file.html HTTP/1.1
    Host: <server>
    ```
  

#### **Wireshark Capture Example**
- **Text Sent by Browser**: Captured requests such as `GET / HTTP/1.1` and additional headers.
- **Response from Web Server**: Server sends back the requested data, often including metadata like the server version and the last modification time.


#### **Summary**
- HTTP/HTTPS protocols are used to transfer data between browsers and web servers.
- Common methods like **GET**, **POST**, **PUT**, and **DELETE** define the operations performed on the server.
- We can use **Wireshark** and **Telnet** to examine and troubleshoot the communication between the client and server, including inspecting headers and responses.

---
---


### File Transfer Protocol (FTP)


#### **FTP Overview**
- **Purpose**: FTP is used for transferring files between a client and a server, unlike HTTP, which is focused on web pages.
- **Efficiency**: FTP typically offers faster file transfers than HTTP under similar conditions.


#### **Common FTP Commands**
1. **USER**: Used to input the username (e.g., `USER anonymous`).
2. **PASS**: Used to provide the password (e.g., `PASS [password]`).
3. **RETR**: Retrieves (downloads) a file from the FTP server to the client (e.g., `RETR coffee.txt`).
4. **STOR**: Stores (uploads) a file from the client to the FTP server (e.g., `STOR file.txt`).


#### **Default FTP Port**
- **Control connection**: FTP uses **TCP port 21** by default for command communication.
- **Data transfer**: Data is transferred over a separate connection between the client and server.


#### **Example FTP Session**
1. **Connecting to FTP Server**: 
   - `ftp MACHINE_IP` to initiate a connection.
   - Login with username `anonymous` (no password needed).
2. **Listing Files**:
   - `ls` to list available files for download.
3. **Switching Transfer Mode**:
   - `type ascii` switches to ASCII mode (for text files).
4. **Downloading File**:
   - `get coffee.txt` downloads the file `coffee.txt`.


#### **Wireshark Capture**
- **FTP Commands**: Commands like `ls` and `get` are exchanged between the client and server.
  - `ls` becomes `LIST` in the communication.
  - Data for files like `coffee.txt` is transferred over a separate connection (Passive Mode).
- **Transfer Mode Warning**: When transferring files in ASCII mode, warnings may appear about linefeed characters, which can cause file corruption in some cases.


#### **Passive Mode**
- FTP uses **Passive Mode** for data transfer, where the server opens a port for data communication and the client connects to it. This is often used when the client is behind a firewall.


#### **Summary**
- **FTP** is designed for efficient file transfers between client and server.
- **Common commands** like `USER`, `PASS`, `RETR`, and `STOR` manage file operations.
- **Wireshark** captures the command exchanges between the client and server, including file transfers and directory listings over separate connections.

---
---


### Simple Mail Transfer Protocol (SMTP)


#### **SMTP Overview**
- **Purpose**: SMTP is used for sending emails between mail clients and mail servers. It also handles mail delivery between different mail servers.
- **Analogy**: SMTP is like visiting a post office to send a package. You provide sender and recipient information, and the server (like a post office) delivers the email.


#### **Common SMTP Commands**
1. **HELO/EHLO**: Initiates an SMTP session (e.g., `HELO client.thm`).
   - **EHLO** is an extended version of **HELO** and is used to request additional features from the server.
2. **MAIL FROM**: Specifies the sender’s email address (e.g., `MAIL FROM: <user@client.thm>`).
3. **RCPT TO**: Specifies the recipient’s email address (e.g., `RCPT TO: <strategos@server.thm>`).
4. **DATA**: Indicates the start of the email message body.
   - The email body follows the `DATA` command, and it ends with a `.` on a line by itself.
5. **QUIT**: Ends the SMTP session (e.g., `QUIT`).


#### **SMTP Default Port**
- **Port 25**: SMTP typically listens on **TCP port 25** for communication between mail clients and servers, or between servers.


#### **Example SMTP Session Using Telnet**
1. **Connecting to the SMTP Server**: 
   - `telnet MACHINE_IP 25` connects to the server using port 25.
2. **Initiating the Session**:
   - `HELO client.thm` starts the SMTP session.
3. **Sending the Email**:
   - `MAIL FROM: <user@client.thm>` and `RCPT TO: <strategos@server.thm>` specify the sender and recipient.
   - The **DATA** command is followed by the email content.
   - The email is ended with a `.` on a new line.
4. **Closing the Connection**: 
   - `QUIT` closes the session.


#### **Wireshark Capture**
- **Wireshark** captures the communication between the client and server.
   - Client messages are shown in **red**, and server responses in **blue**.
   - The **SMTP commands** such as `HELO`, `MAIL FROM`, `RCPT TO`, and `DATA` can be seen in the capture.


#### **SMTP Email Sending Process**
1. **Client sends commands** to initiate the session, specify sender/recipient, and transfer the email message.
2. **Server processes commands**, validates sender and recipient, and accepts or rejects the email.
3. **Finalization** happens with a `QUIT` command to end the session.


#### **Conclusion**
- **SMTP** is an essential protocol for sending emails, handling everything from client-server communication to email delivery.
- The process may seem simple, but it's crucial for understanding how email systems work and for troubleshooting email issues.

---
---


### Post Office Protocol (POP3) - Receiving Email


#### **POP3 Overview**
- **Purpose**: POP3 is used by email clients to retrieve emails from a mail server and download them to a local device.
- **Analogy**: SMTP is like sending a package to the post office, while POP3 is like checking your mailbox for incoming mail.


#### **Common POP3 Commands**
1. **USER <username>**: Identifies the user (e.g., `USER strategos`).
2. **PASS <password>**: Provides the user's password for authentication.
3. **STAT**: Requests the number of messages and the total size of the mailbox.
4. **LIST**: Lists all messages and their sizes.
5. **RETR <message_number>**: Retrieves the specified message by its number (e.g., `RETR 3`).
6. **DELE <message_number>**: Marks a message for deletion.
7. **QUIT**: Ends the POP3 session and applies changes (such as deletions).


#### **POP3 Default Port**
- **Port 110**: POP3 typically listens on **TCP port 110** for client-server communication.


#### **Example POP3 Session Using Telnet**
1. **Connecting to the POP3 Server**: 
   - `telnet MACHINE_IP 110` connects to the server using port 110.
2. **Authentication**:
   - `USER strategos` identifies the user, followed by the `PASS` command to provide the password.
3. **Requesting Mailbox Info**:
   - `STAT` provides the number of messages and total mailbox size.
   - `LIST` displays all messages in the mailbox with their respective sizes.
4. **Retrieving a Message**:
   - `RETR 3` retrieves the third message from the list and displays its content.
5. **Ending the Session**: 
   - `QUIT` closes the connection.


#### **Wireshark Capture**
- **Wireshark** captures the communication between the POP3 client and server.
   - **Red** indicates the client's messages, and **blue** shows the server’s responses.
   - **Sensitive Data**: The **username and password** can be intercepted by someone monitoring the network.


#### **POP3 Email Retrieval Process**
1. **Client connects to the server** and authenticates using the `USER` and `PASS` commands.
2. **Client requests information** about the mailbox using `STAT` and `LIST`.
3. **Client retrieves an email** using the `RETR` command.
4. **Session is closed** with the `QUIT` command.


#### **Security Considerations**
- POP3 communication is **not encrypted by default**, meaning credentials and emails can be intercepted if someone is monitoring the network.
- To enhance security, consider using **POP3S (POP3 over SSL)** or other secure methods like **IMAPS**.

---
---


### Internet Message Access Protocol (IMAP) - Synchronizing Email


#### **IMAP Overview**
- **Purpose**: IMAP allows for the synchronization of email across multiple devices. Unlike POP3, which downloads and deletes emails from the server, IMAP keeps the emails on the server and synchronizes them across clients.
- **Ideal Use Case**: IMAP is perfect for users who access their email from multiple devices, such as desktop computers, smartphones, or laptops.

#### **Key Differences from POP3**
- **POP3**: Downloads and deletes emails from the server.
- **IMAP**: Emails are stored on the server and synchronized with all clients (e.g., marking emails as read on one device reflects across all devices).

#### **Common IMAP Commands**
1. **LOGIN <username> <password>**: Authenticates the user.
2. **SELECT <mailbox>**: Selects the mailbox (e.g., `inbox`) to work with.
3. **FETCH <mail_number> <data_item_name>**: Fetches specific data (e.g., `FETCH 3 body[]` to retrieve message number 3, including both header and body).
4. **MOVE <sequence_set> <mailbox>**: Moves the specified messages to another mailbox.
5. **COPY <sequence_set> <data_item_name>**: Copies messages to another mailbox.
6. **LOGOUT**: Logs the user out of the IMAP server.


#### **IMAP Default Port**
- **Port 143**: IMAP listens on **TCP port 143** by default.

#### **Example IMAP Session Using Telnet**
1. **Connecting to the IMAP Server**: 
   - `telnet MACHINE_IP 143` connects to the server on port 143.
2. **Authentication**: 
   - `LOGIN strategos` authenticates the user.
3. **Selecting the Mailbox**: 
   - `SELECT inbox` selects the inbox to interact with.
4. **Fetching a Message**: 
   - `FETCH 3 body[]` retrieves the content of message 3, including both the header and the body.
5. **Logging Out**: 
   - `LOGOUT` ends the session and logs the user out of the IMAP server.


#### **Wireshark Capture**
- **Wireshark** captures the communication between the IMAP client and server.
   - **Client’s Commands**: Displayed in **red**.
   - **Server’s Responses**: Displayed in **blue**.


#### **IMAP Email Synchronization Process**
1. **Client connects** to the IMAP server and authenticates using `LOGIN`.
2. **Client selects** the desired mailbox using `SELECT` (e.g., `inbox`).
3. **Client fetches** a specific message using `FETCH`.
4. **Session is ended** with the `LOGOUT` command.


#### **Security Considerations**
- **IMAPS (IMAP over SSL/TLS)** should be used for secure communication to prevent interception of credentials and email content.


#### **Wireshark Capture Insights**
- The **commands** sent by the client are minimal (only four commands in this example).
- The **server’s responses** are more detailed and contain the message data, such as the email headers and body.

---
---


| **Protocol** | **Transport Protocol** | **Default Port Number** |
|--------------|------------------------|-------------------------|
| TELNET       | TCP                    | 23                      |
| DNS          | UDP or TCP             | 53                      |
| HTTP         | TCP                    | 80                      |
| HTTPS        | TCP                    | 443                     |
| FTP          | TCP                    | 21                      |
| SMTP         | TCP                    | 25                      |
| POP3         | TCP                    | 110                     |
| IMAP         | TCP                    | 143                     |


#### **Key Points:**
- **TELNET (Port 23)**: A simple protocol used for remote access to servers.
- **DNS (Port 53)**: Used for domain name resolution, typically over UDP but can also operate over TCP.
- **HTTP (Port 80)**: The protocol for serving web pages over the internet.
- **HTTPS (Port 443)**: The secure version of HTTP, utilizing SSL/TLS encryption.
- **FTP (Port 21)**: Used for transferring files between a client and server.
- **SMTP (Port 25)**: Used for sending emails between mail servers.
- **POP3 (Port 110)**: Used for retrieving emails from a server to a client, downloading and deleting them.
- **IMAP (Port 143)**: Allows email clients to access and synchronize email stored on a server.
