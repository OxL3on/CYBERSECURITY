### **Web Application Overview** 🌐

#### **1. Web Application as a Planet 🌍**
- **Analogy**: A web app is like a planet.
  - **Surface (Front End)**: What users see and interact with (like a browser).
  - **Under the Surface (Back End)**: Hidden systems that make everything work (like gravity or air).


#### **2. Front End: The Surface of the Planet**
- **HTML**: The basic structure of the planet (like DNA for simple organisms). It tells the browser what to display.
  - Example: A gray, bare planet without design or movement.
- **CSS**: Adds colors, styles, and layouts to the planet (like DNA for appearance).
  - Example: A vibrant, colorful planet with textures and patterns.
- **JavaScript**: Adds interactivity and decision-making (like the brain of an advanced organism).
  - Example: A planet where things move and react based on user actions.


#### **3. Back End: The Hidden Systems**
- **Database**: Stores and manages data (like a planet’s library or filing system).
  - Example: Stores user preferences or login details.
- **Infrastructure**: The systems that keep the app running (like roads, cars, and fuel on a planet).
  - Includes web servers, storage, and networking.
- **WAF (Web Application Firewall)**: Protects the app from harmful requests (like a planet’s ozone layer blocking UV rays).


#### **4. Summary**
- **Front End**: What users see and interact with (HTML, CSS, JavaScript).
- **Back End**: The hidden systems that make the app work (database, servers, WAF).

---
---


### **Uniform Resource Locator (URL)** 🌐


#### **1. What is a URL?**
- A **URL** is a web address that helps your browser find online content like webpages, videos, or photos.
- Think of it as a map guiding your browser to the right place on the internet.


#### **2. Anatomy of a URL**
A URL is made up of several parts, each with a specific role:

1. **Scheme**:
   - The **protocol** used to access the website (e.g., `HTTP` or `HTTPS`).
   - **HTTPS** is more secure because it encrypts the connection.
   - Example: `https://` (secure) vs. `http://` (not secure).

2. **User**:
   - Rarely used, but some URLs include a **username** for authentication.
   - Example: `username@example.com`.
   - **Warning**: Including login details in URLs is unsafe and not common.

3. **Host/Domain**:
   - The **website’s address** (e.g., `google.com`).
   - Domains must be unique and are registered through domain registrars.
   - **Watch out for fake domains** (typosquatting) used in phishing attacks.

4. **Port**:
   - A number that directs your browser to the right service on the server.
   - Common ports: `80` for HTTP, `443` for HTTPS.
   - Example: `example.com:443`.

5. **Path**:
   - Points to a specific **file or page** on the server.
   - Example: `/blog/post-1` leads to a blog post.
   - **Security Tip**: Protect paths to restrict access to sensitive resources.

6. **Query String**:
   - Starts with a `?` and includes **search terms or inputs**.
   - Example: `?search=web+development`.
   - **Security Tip**: Handle query strings carefully to prevent injection attacks.

7. **Fragment**:
   - Starts with a `#` and points to a **specific section** of a webpage.
   - Example: `#section-2` jumps to a heading or table.
   - **Security Tip**: Clean up fragments to avoid injection risks.


#### **3. Why URLs Matter**
- URLs help you navigate the web and access resources.
- Understanding their parts is crucial for:
  - **Browsing**: Knowing where you’re going.
  - **Development**: Building and troubleshooting web apps.
  - **Security**: Avoiding phishing and injection attacks.


#### **4. Example URL Breakdown**
- **URL**: `https://www.example.com:443/blog/post-1?search=web#section-2`
  - **Scheme**: `https://`
  - **Host/Domain**: `www.example.com`
  - **Port**: `:443`
  - **Path**: `/blog/post-1`
  - **Query String**: `?search=web`
  - **Fragment**: `#section-2`

---
---



### **HTTP Messages** 🌐

#### **1. What are HTTP Messages?**
- **HTTP Messages** are packets of data exchanged between a **client** (user) and a **server**.
- They are the backbone of how web apps communicate.
- Two types:
  1. **HTTP Requests**: Sent by the user to trigger actions (e.g., loading a page, submitting a form).
  2. **HTTP Responses**: Sent by the server in reply to the user’s request.


#### **2. Structure of HTTP Messages**
Every HTTP message has four main parts:

1. **Start Line**:
   - The **introduction** of the message.
   - In a **request**, it includes:
     - **Method**: What action to perform (e.g., `GET`, `POST`).
     - **URL**: The resource being requested.
   - In a **response**, it includes:
     - **Status Code**: The result of the request (e.g., `200 OK`, `404 Not Found`).

2. **Headers**:
   - Key-value pairs that provide **extra information** about the message.
   - Examples:
     - `Content-Type`: Specifies the type of data (e.g., `text/html`, `application/json`).
     - `Authorization`: Includes credentials for secure access.
   - Help with security, content handling, and more.

3. **Empty Line**:
   - A blank line that **separates headers from the body**.
   - Ensures the message is interpreted correctly.

4. **Body**:
   - Contains the **actual data** being sent or received.
   - In a **request**: Includes data like form inputs or file uploads.
   - In a **response**: Contains the requested content (e.g., HTML, JSON).


#### **3. Example: HTTP Request and Response**
- **HTTP Request**:
  ```
  POST /login HTTP/1.1
  Host: example.com
  Content-Type: application/json
  Authorization: Bearer token123

  {"username": "user", "password": "pass"}
  ```
  - **Start Line**: `POST /login HTTP/1.1` (method, path, protocol).
  - **Headers**: `Host`, `Content-Type`, `Authorization`.
  - **Body**: `{"username": "user", "password": "pass"}`.

- **HTTP Response**:
  ```
  HTTP/1.1 200 OK
  Content-Type: application/json

  {"message": "Login successful"}
  ```
  - **Start Line**: `HTTP/1.1 200 OK` (protocol, status code, message).
  - **Headers**: `Content-Type`.
  - **Body**: `{"message": "Login successful"}`.


#### **4. Why HTTP Messages Matter**
- **Foundation of Web Communication**: They enable smooth interaction between clients and servers.
- **Troubleshooting**: Understanding them helps diagnose issues (e.g., why a page isn’t loading).
- **Security**: Proper handling prevents attacks like data tampering or injection.

---
---


### **HTTP Request: Request Line and Methods** 🌐


#### **1. What is an HTTP Request?**
- An **HTTP request** is sent by a user (client) to a server to interact with a web application.
- It’s the first point of contact between the user and the server, making it crucial for **security** and functionality.


#### **2. Request Line**
- The **first line** of an HTTP request, also called the **start line**.
- Format: `METHOD /path HTTP/version`
  - **Method**: What action to perform (e.g., `GET`, `POST`).
  - **Path**: The resource being requested (e.g., `/login`).
  - **Version**: The HTTP protocol version (e.g., `HTTP/1.1`).


#### **3. HTTP Methods**
- Define the **action** the user wants to perform on the server.
- Common methods and their **security considerations**:

1. **GET**:
   - Fetches data from the server.
   - **Security Tip**: Avoid exposing sensitive data (e.g., tokens, passwords) in URLs.

2. **POST**:
   - Sends data to the server (e.g., form submissions).
   - **Security Tip**: Validate and sanitize inputs to prevent attacks like **SQL injection** or **XSS**.

3. **PUT**:
   - Updates or replaces a resource on the server.
   - **Security Tip**: Ensure only authorized users can make changes.

4. **DELETE**:
   - Removes a resource from the server.
   - **Security Tip**: Restrict access to authorized users only.

5. **PATCH**:
   - Updates part of a resource.
   - **Security Tip**: Validate data to avoid inconsistencies.

6. **HEAD**:
   - Retrieves only headers, not the full content.
   - Useful for checking metadata.

7. **OPTIONS**:
   - Lists available methods for a resource.
   - **Security Tip**: Disable if not needed to reduce attack surface.

8. **TRACE**:
   - Used for debugging (shows allowed methods).
   - **Security Tip**: Often disabled for security reasons.

9. **CONNECT**:
   - Creates a secure connection (e.g., for HTTPS).
   - Critical for encrypted communication.

#### **4. URL Path**
- Specifies the **resource** being requested (e.g., `/api/users/123`).
- **Security Tips**:
  - Validate paths to prevent unauthorized access.
  - Sanitize paths to avoid **injection attacks**.
  - Protect sensitive data with privacy and risk assessments.


#### **5. HTTP Version**
- Indicates the **protocol version** used for communication.
- Common versions:
  1. **HTTP/0.9** (1991): Only supported `GET` requests.
  2. **HTTP/1.0** (1996): Added headers and better content support.
  3. **HTTP/1.1** (1997): Introduced persistent connections and better caching (still widely used).
  4. **HTTP/2** (2015): Added multiplexing, header compression, and prioritization for faster performance.
  5. **HTTP/3** (2022): Uses **QUIC** for quicker, more secure connections.

- **Upgrade Tip**: Moving to HTTP/2 or HTTP/3 improves speed and security.


#### **6. Why This Matters**
- **Foundation of Web Communication**: Understanding requests helps build and secure web apps.
- **Security**: Proper handling prevents attacks like injection, unauthorized access, and data exposure.
- **Performance**: Upgrading HTTP versions can enhance speed and reliability.

---
---


### HTTP Request: Headers and Body

#### **Request Headers**
- **What are they?**
  - Extra info sent to the web server about the request.
  
- **Common Headers:**
  1. **Host**: 
     - *Example*: `Host: tryhackme.com`
     - *What it does*: Tells the server which website you're asking for.
     
  2. **User-Agent**: 
     - *Example*: `User-Agent: Mozilla/5.0`
     - *What it does*: Tells the server what browser or device you're using.
     
  3. **Referer**: 
     - *Example*: `Referer: https://www.google.com/`
     - *What it does*: Shows where the request came from (like a referral link).
     
  4. **Cookie**: 
     - *Example*: `Cookie: user_type=student; room=introtowebapplication; room_status=in_progress`
     - *What it does*: Sends small pieces of data (like login info) stored by the browser.
     
  5. **Content-Type**: 
     - *Example*: `Content-Type: application/json`
     - *What it does*: Tells the server what kind of data is being sent (e.g., JSON, XML).


#### **Request Body**
- **What is it?**
  - The part of the HTTP request that contains the actual data being sent to the server (used in POST/PUT requests).
  
- **Common Data Formats:**

  1. **URL Encoded (`application/x-www-form-urlencoded`)**:
     - *Structure*: `key=value&key2=value2`.
     - *Example*: Sending user info like `name=Aleksandra&age=27&country=US`.
     - *When used?* Simple forms or small data.

  2. **Form Data (`multipart/form-data`)**:
     - *Structure*: Data split into blocks separated by a boundary.
     - *Example*: Uploading files like images.
       ```plaintext
       ----WebKitFormBoundary7MA4YWxkTrZu0gW
       Content-Disposition: form-data; name="username"
       aleksandra
       ----WebKitFormBoundary7MA4YWxkTrZu0gW
       Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
       ```
     - *When used?* When uploading files or sending large amounts of data.

  3. **JSON (`application/json`)**:
     - *Structure*: Data in key-value pairs inside `{}`.
     - *Example*: 
       ```json
       {
           "name": "Aleksandra",
           "age": 27,
           "country": "US"
       }
       ```
     - *When used?* APIs often use JSON to send structured data.

  4. **XML (`application/xml`)**:
     - *Structure*: Data inside tags like `<tag>value</tag>`.
     - *Example*: 
       ```xml
       <user>
           <name>Aleksandra</name>
           <age>27</age>
           <country>US</country>
       </user>
       ```
     - *When used?* Older systems or specific APIs may use XML.


#### **Quick Story Example**
Imagine you're ordering a pizza online:

- **Headers** are like telling the pizza place your address (`Host`), how you ordered (via phone or app - `User-Agent`), and if you have a coupon (`Cookie`).
- **Body** is the actual order:
  - If you're ordering via text, you might say: `size=large&toppings=pepperoni` (URL Encoded).
  - If you're uploading a picture of your custom pizza design, you'd use `multipart/form-data`.
  - If you're using an app, it might send your order as JSON: 
    ```json
    {
        "size": "large",
        "toppings": ["pepperoni", "mushrooms"]
    }
    ```

---
---


### HTTP Response: Status Line and Status Codes

#### **What is an HTTP Response?**
- When you interact with a web app, the server sends back an **HTTP response** to let you know if your request worked or if something went wrong.
- The response includes:
  - **Status Code**: A three-digit number that tells you the result of your request.
  - **Reason Phrase**: A short explanation of the status code (e.g., "OK", "Not Found").


#### **Status Line**
- The **first line** of every HTTP response.
- Contains three key pieces of info:
  1. **HTTP Version**: Which version of HTTP is being used (e.g., HTTP/1.1).
  2. **Status Code**: A three-digit number indicating success or failure.
  3. **Reason Phrase**: A human-readable message explaining the status code.


#### **Status Code Categories**
Status codes are grouped into five main categories:

1. **100-199: Informational Responses**
   - The server received part of the request and is waiting for the rest.
   - Example: `100 Continue` — The server is ready for the next part of the request.

2. **200-299: Successful Responses**
   - Everything worked as expected.
   - Example: `200 OK` — The request was successful, and the server sent back the requested data.

3. **300-399: Redirection Messages**
   - The resource has moved to a new location.
   - Example: `301 Moved Permanently` — The resource is now at a new URL; use that from now on.

4. **400-499: Client Error Responses**
   - There’s a problem with the request (e.g., wrong URL, missing info).
   - Example: `404 Not Found` — The server couldn’t find the resource at the given URL.

5. **500-599: Server Error Responses**
   - Something went wrong on the server’s end.
   - Example: `500 Internal Server Error` — The server had an issue processing the request.


#### **Common Status Codes**
Here are some frequently seen status codes:

- **100 Continue**: The server got the first part of the request and is ready for more.
- **200 OK**: The request was successful, and the server sent back the requested data.
- **301 Moved Permanently**: The resource has moved to a new URL permanently.
- **404 Not Found**: The server couldn’t find the resource at the given URL.
- **500 Internal Server Error**: Something went wrong on the server’s side.


#### **Quick Story Example**
Imagine you're ordering food online:

- **200 OK**: Your order was successful, and the food is on its way!
- **404 Not Found**: You tried to order from a restaurant that doesn’t exist anymore.
- **500 Internal Server Error**: The food delivery app crashed while processing your order.
- **301 Moved Permanently**: The restaurant moved to a new location, so you need to update your address book.
- **100 Continue**: You started placing an order, and the app is waiting for you to finish adding items.

---
---


### HTTP Response: Headers and Body

#### **Response Headers**
- **What are they?**
  - Key-value pairs sent by the server to provide important info about the response.
  - They tell the client (e.g., browser) how to handle the response.


#### **Required Response Headers**
These headers are crucial for proper communication between the server and client:

1. **Date**:
   - *Example*: `Date: Fri, 23 Aug 2024 10:43:21 GMT`
   - *What it does*: Shows when the response was generated by the server.

2. **Content-Type**:
   - *Example*: `Content-Type: text/html; charset=utf-8`
   - *What it does*: Tells the client what kind of content is being sent (e.g., HTML, JSON) and the character set (e.g., UTF-8).

3. **Server**:
   - *Example*: `Server: nginx`
   - *What it does*: Reveals the server software handling the request. Useful for debugging but can be a security risk if exposed.


#### **Other Common Response Headers**
These headers provide additional instructions to the client or browser:

1. **Set-Cookie**:
   - *Example*: `Set-Cookie: sessionId=38af1337es7a8`
   - *What it does*: Sends cookies to the client. Use flags like `HttpOnly` (prevents JavaScript access) and `Secure` (only sent over HTTPS) for better security.

2. **Cache-Control**:
   - *Example*: `Cache-Control: max-age=600`
   - *What it does*: Controls how long the client can cache the response. Use `no-cache` to prevent sensitive data from being cached.

3. **Location**:
   - *Example*: `Location: /index.html`
   - *What it does*: Used in redirection responses (e.g., 3xx). Be careful with user-modifiable headers to avoid open redirect vulnerabilities.



#### **Response Body**
- **What is it?**
  - The part of the HTTP response that contains the actual data sent by the server (e.g., HTML, JSON, images).
  
- **Security Tip**:
  - Always sanitise and escape user-generated content before including it in the response body to prevent attacks like Cross-Site Scripting (XSS).


#### **Quick Story Example**
Imagine you're downloading a file from a website:

- **Headers**:
  - `Content-Type: application/pdf` tells your browser it's a PDF file.
  - `Cache-Control: max-age=3600` tells your browser it can cache the file for an hour.
  - `Set-Cookie: sessionId=abc123` gives your browser a session ID to remember you.

- **Body**:
  - The actual PDF file is sent in the response body. If the file name came from user input, the server must sanitise it to avoid malicious scripts.

---
---


### Security Headers

#### **What are Security Headers?**
- HTTP Security Headers help protect web applications from common attacks like **Cross-Site Scripting (XSS)**, **clickjacking**, and others.
- These headers provide additional layers of security to control how browsers handle content and data.

You can use tools like [securityheaders.io](https://securityheaders.io/) to check the security headers of any website.


### **Key Security Headers**

#### 1. **Content-Security-Policy (CSP)**
- **Purpose**: Protects against **XSS** and other code injection attacks by specifying which sources of content are trusted.
- **Example**:
  ```http
  Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'
  ```
- **Breakdown**:
  - `default-src 'self'`: Only allow content from the same domain as the website.
  - `script-src 'self' https://cdn.tryhackme.com`: Allow scripts from the same domain and a specific CDN.
  - `style-src 'self'`: Only allow CSS from the same domain.
- **Why it matters**: Prevents malicious scripts or styles from being loaded from untrusted sources.


#### 2. **Strict-Transport-Security (HSTS)**
- **Purpose**: Ensures that browsers always connect over **HTTPS** (secure connection).
- **Example**:
  ```http
  Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
  ```
- **Breakdown**:
  - `max-age=63072000`: The browser will enforce HTTPS for 2 years (in seconds).
  - `includeSubDomains`: Applies HTTPS to all subdomains.
  - `preload`: Allows the site to be added to browser preload lists for automatic HTTPS enforcement.
- **Why it matters**: Prevents attackers from intercepting traffic via insecure HTTP connections.


#### 3. **X-Content-Type-Options**
- **Purpose**: Prevents browsers from guessing the **MIME type** of a resource (MIME sniffing).
- **Example**:
  ```http
  X-Content-Type-Options: nosniff
  ```
- **Breakdown**:
  - `nosniff`: Forces the browser to only use the `Content-Type` header to determine the file type.
- **Why it matters**: Stops attackers from tricking the browser into executing malicious files (e.g., running a script disguised as an image).


#### 4. **Referrer-Policy**
- **Purpose**: Controls how much **referrer information** is sent when navigating between websites.
- **Examples**:
  - `Referrer-Policy: no-referrer`: No referrer info is sent.
  - `Referrer-Policy: same-origin`: Referrer info is only sent for links within the same site.
  - `Referrer-Policy: strict-origin`: Referrer info is only sent when the protocol stays the same (e.g., HTTPS → HTTPS).
  - `Referrer-Policy: strict-origin-when-cross-origin`: Sends full URL for same-origin requests but only the origin for cross-origin requests.
- **Why it matters**: Protects user privacy by limiting how much referrer data is shared with external sites.

### **Quick Story Example**
Imagine you're running a secure online store:

- **CSP**: You set up a CSP to ensure only your website and trusted CDNs can load scripts and styles. This prevents attackers from injecting malicious scripts.
- **HSTS**: You enable HSTS to make sure customers always connect securely via HTTPS, even if they accidentally type "http" in the address bar.
- **X-Content-Type-Options**: You add `nosniff` to stop browsers from misinterpreting files (e.g., treating an image as a script).
- **Referrer-Policy**: You use `strict-origin-when-cross-origin` to protect customer privacy when they click links to external sites.
