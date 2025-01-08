### Introduction to Active Directory

**Active Directory (AD):**  
Think of Active Directory as the "brain" of a corporate network, where all the users, computers, and policies are centrally managed. It's like a headquarters for controlling everything in a business's digital world.

#### Why Active Directory Matters:
Imagine you're managing a small business network:  
- **Small Network:** You can manually set up 5 computers and users without much hassle.  
- **Big Network:** Now imagine you have 157 computers and 320 users spread across 4 offices. Managing everything manually becomes nearly impossible.

**Solution:**  
Use a **Windows Domain** powered by Active Directory.  
- **Windows Domain:** A group of computers and users managed under one system.  
- **Active Directory (AD):** The central "hub" for managing this domain.  
- **Domain Controller (DC):** The server running AD that keeps everything in sync.

#### Benefits of a Windows Domain:
1. **Centralized Management:**  
   - Manage all users, computers, and settings in one place.  
   - Example: Create a new user in AD, and they can log into any computer in the domain without setting them up on each device.

2. **Policy Control:**  
   - Configure and apply security rules across the network from one place.  
   - Example: Restrict access to sensitive settings (like the control panel) for students or employees.

#### Real-Life Example:
Ever logged into a school or office computer with a username and password?  
- **How it Works:** When you log in, the computer sends your credentials to the AD server for verification.  
- **Why it’s Useful:** Your account works on any computer in the network without needing separate setups.

**Policies in Action:**  
- Schools often block students from accessing admin settings. This is done by deploying policies through AD, making sure no student can change system settings.

---
---

### Understanding Active Directory Domain Services (AD DS)

**What is AD DS?**  
Active Directory Domain Services (AD DS) is like a digital catalog that holds information about everything in a network. These "things" are called **objects**, and they include users, machines, printers, and more.

#### Key Objects in AD DS

1. **Users:**  
   - **Who are they?** People or services in the network.  
     - Example:  
       - Employees like "Alice" or "Bob."  
       - Services like MSSQL (special accounts created for programs).  
   - **What can they do?** Users can be authenticated (log in) and assigned privileges, like accessing files or printers.  
   - **Fun Fact:** Service users are different—they only get the permissions needed for their tasks.

2. **Machines:**  
   - **What are they?** Every computer in the domain gets its own object in AD.  
   - **Special Features:**  
     - Machine accounts are like users for computers, but their passwords (120 random characters!) change automatically.  
     - **Naming:** The account name ends with a `$` (e.g., `DC01$`).  
   - **Who uses them?** Generally, the computer itself. But if you have the password, you could log in too!

3. **Security Groups:**  
   - **Why are they useful?** Assign access to many users or machines at once.  
     - Example: Instead of giving "Alice" and "Bob" access to a printer one by one, put them in the "PrinterAccess" group.  
   - **Default Groups:**  
     - **Domain Admins:** Full control over the domain.  
     - **Backup Operators:** Access all files to perform backups.  
     - **Domain Users:** Includes all users in the domain.  
     - Many more, depending on your needs.

#### Organizing with OUs (Organizational Units)

1. **What are OUs?**  
   OUs are folders that help classify users and computers into logical groups, like departments in a company (e.g., IT, Sales).

2. **Why OUs?**  
   - Policies (rules) can be applied to all users in an OU.  
     - Example: IT users might need admin privileges, while Sales users don't.  
   - **Note:** A user can belong to only one OU at a time.

3. **How do OUs look in action?**  
   - Example: In the domain "THM.local," there's an OU for "THM" with child OUs like IT, Management, Marketing, and Sales.  
   - You can create new OUs (e.g., "Students") to organize users as needed.

#### OUs vs. Security Groups

- **OUs:**  
  - Used for applying policies (e.g., restrictions, software setups).  
  - One user = One OU.  

- **Security Groups:**  
  - Used for permissions (e.g., shared folder access).  
  - One user = Can belong to multiple groups.  

#### Managing AD DS

1. **Access Tool:** "Active Directory Users and Computers" (ADUC).  
2. **What You Can Do:**  
   - Create, delete, and modify users or groups.  
   - Reset passwords (a common helpdesk task).  
   - Move machines to specific OUs for better organization.  
3. **Default Containers:**  
   - **Builtin:** Predefined groups (e.g., Admins).  
   - **Computers:** Holds new machines joining the network.  
   - **Users:** Domain-wide users and groups.

**Summary:** AD DS helps centralize and organize network objects like users, machines, and groups. By combining OUs (for policies) and Security Groups (for permissions), administrators can efficiently manage everything in a large network.

---
---

### Steps to Manage Active Directory Based on Organizational Chart

#### **1. Review and Adjust OUs (Organizational Units)**  
- **Task:** Identify and delete the extra department OU.
- **Steps to Delete an OU:**
  1. Enable **Advanced Features** in the "View" menu of **Active Directory Users and Computers** (ADUC).
  2. Right-click the extra OU and select **Properties**.
  3. Navigate to the **Object** tab and uncheck **Protect object from accidental deletion**.
  4. Right-click the OU and delete it. Confirm the action, which also deletes all its child objects.

#### **2. Synchronize AD Users with the Organizational Chart**  
- **Task:** Create or delete users to match the chart.
- **Steps:**
  1. Open ADUC and navigate to the relevant OU.
  2. To delete users:
     - Right-click the user and select **Delete**.
  3. To create users:
     - Right-click the OU and select **New > User**.
     - Fill in the user details (e.g., first name, last name, username).
     - Set a temporary password (users can reset this upon login).

#### **3. Delegate Control to Phillip for IT Support**  
- **Task:** Allow Phillip to reset passwords for users in specific OUs (Sales, Marketing, Management).  
- **Steps to Delegate Control:**
  1. Right-click the target OU (e.g., Sales) and select **Delegate Control**.
  2. Add Phillip as the delegate:
     - Type "phillip" and click **Check Names** to verify.
  3. Choose **Reset user passwords and force password change at next logon**.
  4. Complete the wizard.

#### **4. Reset Sophie's Password as Phillip**  
- **Task:** Use PowerShell to reset Sophie's password and enforce a password change at the next logon.
- **Steps:**
  1. Log in as Phillip using RDP with the following credentials:
     - **Username:** `THM\phillip`  
     - **Password:** `Claire2008`
  2. Open PowerShell and execute:
     - **Reset password:**  
       ```powershell
       Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
       ```
     - **Force password change at next logon:**  
       ```powershell
       Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose
       ```
       
#### **5. Log in as Sophie and Retrieve the Flag**  
- **Task:** Use Sophie's account to log in and find the flag on her desktop.  
- **Steps:**
  1. Log in via RDP using:
     - **Username:** `THM\sophie`  
     - **Password:** The new password you set.
  2. Navigate to Sophie's desktop to retrieve the flag.

### Key Commands Recap
- **Reset a User's Password:**  
  ```powershell
  Set-ADAccountPassword <username> -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
  ```
- **Force Password Change at Next Logon:**  
  ```powershell
  Set-ADUser -ChangePasswordAtLogon $true -Identity <username> -Verbose
  ``` 

**Goal:** Ensure the AD configuration matches the organizational chart, delegate appropriate privileges, and successfully reset Sophie's password to retrieve the flag.

---
---


### Steps to Organize Machines in Active Directory

To properly segregate devices in Active Directory, follow these steps:

#### **1. Create OUs for Workstations and Servers**
- **Task:** Create two new Organizational Units (OUs) under the domain container (`thm.local`).
- **Steps:**
  1. Open **Active Directory Users and Computers (ADUC)**.
  2. Right-click the domain name (`thm.local`) and select **New > Organizational Unit**.
  3. Create the first OU named **Workstations**.
  4. Repeat the process to create a second OU named **Servers**.
  
After completion, your structure should look like this:
```
thm.local
├── Workstations
├── Servers
├── Domain Controllers (default)
```

#### **2. Move Devices to the Appropriate OUs**
- **Task:** Organize the machines in the "Computers" container into the new OUs based on their roles.  
- **Steps:**
  1. In ADUC, navigate to the **Computers** container.
  2. Identify each machine's role:
     - Personal computers and laptops → Move to **Workstations**.
     - Servers → Move to **Servers**.
  3. Right-click the machine and select **Move**.
  4. Choose the appropriate OU (Workstations or Servers) and click **OK**.

Repeat this for all devices in the **Computers** container.

#### **3. Verify the New OU Structure**
- **Task:** Confirm that all machines have been correctly moved to their respective OUs.  
- **Steps:**
  1. Navigate to the **Workstations** and **Servers** OUs in ADUC.
  2. Check that:
     - Workstations OU contains personal computers and laptops.
     - Servers OU contains server machines.
     - The **Computers** container is now empty or only contains devices yet to be categorized.

### Benefits of Segregating Machines
1. **Policy Management:** You can apply group policies (GPOs) tailored to Workstations and Servers.
2. **Enhanced Security:** Different policies can enforce stricter controls on servers and domain controllers.
3. **Easier Administration:** Clearly organized OUs make it simpler to manage and audit devices.

---
---

### Implementing and Testing the Required GPOs

#### **1. Restrict Access to Control Panel**

- **Objective:** Block non-IT users (Marketing, Management, and Sales departments) from accessing the Control Panel.
- **Steps:**
  1. Open **Group Policy Management**.
  2. Right-click **Group Policy Objects**, select **New**, and name it **Restrict Control Panel Access**.
  3. Right-click the GPO and select **Edit**.
  4. Navigate to:
     ```
     User Configuration > Policies > Administrative Templates > Control Panel
     ```
  5. Enable **Prohibit Access to Control Panel and PC Settings**.
  6. Close the GPO editor.
  7. Link the GPO to the **Marketing**, **Management**, and **Sales** OUs by dragging and dropping the GPO to each OU.

- **Verification:**
  1. Log in to a machine as **Mark** (Marketing department user).
     - Use credentials: 
       ```
       Username: THM\Mark  
       Password: M4rk3t1ng.21
       ```
  2. Attempt to open the Control Panel. You should see a message denying access.

#### **2. Auto Lock Screen**

- **Objective:** Ensure all computers (workstations, servers, and domain controllers) lock their screens after 5 minutes of inactivity.
- **Steps:**
  1. Open **Group Policy Management**.
  2. Right-click **Group Policy Objects**, select **New**, and name it **Auto Lock Screen**.
  3. Right-click the GPO and select **Edit**.
  4. Navigate to:
     ```
     Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options
     ```
  5. Find **Interactive Logon: Machine Inactivity Limit**, set it to **300 seconds (5 minutes)**, and apply.
  6. Close the GPO editor.
  7. Link the GPO to the **root domain (thm.local)** to apply it to all computers.

- **Verification:**
  1. Log in to a workstation or server and remain inactive for 5 minutes.  
  2. The session should lock automatically after 5 minutes.

### **Force GPO Updates (if needed)**
If the policies don’t seem to apply immediately:
1. Open a command prompt or PowerShell as an administrator.
2. Run the command:
   ```
   gpupdate /force
   ```

### Notes
- **Inheritance:** The Auto Lock Screen policy applies to all computers because it's linked to the root domain, and sub-OUs inherit its settings. Non-computer OUs (like Sales, Marketing, etc.) ignore the policy since it only applies to computers.
- **Testing Users:** IT users should still be able to access the Control Panel, as the **Restrict Control Panel Access** GPO wasn't applied to their OU. Log in as any IT user to verify.

---
---

### Windows Authentication Protocols: Kerberos and NetNTLM

#### **Kerberos Authentication**

- **Overview:** Default authentication protocol for recent versions of Windows domains, utilizing ticket-based authentication.
- **Key Components:**
  - **Key Distribution Center (KDC):** Resides on the Domain Controller; creates tickets.
  - **Tickets:**  
    - **Ticket Granting Ticket (TGT):** Obtained after initial authentication and used to request service-specific tickets.  
    - **Ticket Granting Service (TGS):** Allows access to specific services.

- **Authentication Process:**
  1. **Initial Request:**
     - User sends their username and an encrypted timestamp (using a password-derived key) to the KDC.
  2. **TGT Issuance:**
     - KDC returns a TGT and a Session Key.  
     - TGT is encrypted with the **krbtgt** account's password hash, making it unreadable to the user.
  3. **Service Access:**
     - User requests a TGS by presenting the TGT, SPN (indicating service and server), and an encrypted timestamp.
     - KDC provides a TGS and a Service Session Key.
  4. **Service Connection:**
     - TGS is sent to the target service.
     - Service decrypts the TGS using its account password hash and validates the Service Session Key.

- **Key Points:**
  - TGT avoids the need to send user credentials repeatedly.
  - The Service Owner's hash encrypts the TGS.
  - Secure ticket exchange ensures no sensitive data is transmitted in plaintext.

#### **NetNTLM Authentication**

- **Overview:** Legacy authentication protocol using a challenge-response mechanism.
- **Authentication Process:**
  1. **Client Request:**
     - Client sends an authentication request to the server.
  2. **Challenge Issuance:**
     - Server generates a random number (challenge) and sends it to the client.
  3. **Response Generation:**
     - Client combines the NTLM password hash with the challenge and sends the response to the server.
  4. **Domain Controller Verification:**
     - Server forwards the challenge and response to the Domain Controller.
     - Domain Controller recalculates the response and compares it to the client’s response.
  5. **Result Transmission:**
     - Authentication result is sent to the server, which forwards it to the client.

- **Key Points:**
  - Password or hash is never sent over the network.
  - If using a local account, the server verifies the challenge-response locally via the SAM.

#### **Comparison of Kerberos and NetNTLM**

| **Feature**              | **Kerberos**                         | **NetNTLM**                        |
|--------------------------|--------------------------------------|------------------------------------|
| **Default/Legacy**       | Default                              | Legacy                             |
| **Authentication Basis** | Ticket-based                        | Challenge-response                 |
| **Password Transmission**| Never transmitted                   | Never transmitted                  |
| **Efficiency**           | High (reduced repeated credential use) | Lower (requires Domain Controller interaction per request) |
| **Security**             | Stronger (uses tickets and encryption) | Weaker (vulnerable to relay attacks) |
| **Primary Use Case**     | Modern networks                     | Compatibility with older systems   |


---
---


### Active Directory Multi-Domain Structures

#### **Single Domain**
- **Description:** A single domain is suitable for small organizations, centralizing resources and policies.
- **Limitation:** As the organization grows, managing everything under one domain can become cumbersome, especially when dealing with geographical and regulatory differences.

#### **Trees**
- **Purpose:** To manage multiple domains within the same namespace efficiently.
- **Structure:**
  - Domains in a tree share a common root domain (e.g., `thm.local`).
  - Subdomains can represent different branches or regions, e.g., `uk.thm.local` and `us.thm.local`.
- **Benefits:**
  - Separate management for each domain, reducing complexity.
  - Each domain has its own Domain Controllers (DCs) and policies.
  - IT teams for each domain manage resources independently, ensuring localized control.
- **Security Groups:**
  - **Domain Admins:** Manage resources in their specific domain.
  - **Enterprise Admins:** Have administrative privileges across all domains in the tree.

#### **Forests**
- **Purpose:** To unify multiple domain trees with different namespaces into one network.
- **Structure:** A forest can include several trees, e.g., `thm.local` and `mht.com`.
- **Use Case:** Suitable for organizations that acquire other companies with pre-existing domain structures.
- **Benefits:**
  - Allows organizations to maintain separate namespaces while integrating resources.
  - Each tree operates independently but can be connected via trust relationships for collaboration.

#### **Trust Relationships**
- **Definition:** Trust relationships allow domains to grant cross-domain access to resources.
- **Types of Trust Relationships:**
  1. **One-Way Trust:**  
     - Access flows in one direction.
     - Example: If Domain `AAA` trusts Domain `BBB`, users from `BBB` can access `AAA` resources, but not vice versa.
  2. **Two-Way Trust:**  
     - Mutual access is possible between both domains.
     - Formed automatically when domains are joined under a tree or forest.

- **Key Points:**
  - Trusts enable resource sharing but don’t grant automatic access.
  - Administrators must explicitly authorize cross-domain access to specific resources.

### **Comparison of Trees and Forests**

| **Feature**        | **Trees**                           | **Forests**                          |
|--------------------|------------------------------------|-------------------------------------|
| **Namespace**      | Common (e.g., `thm.local`)         | Different (e.g., `thm.local`, `mht.com`) |
| **Purpose**        | Separate management within a single organization | Integration of different organizations or domains |
| **Trusts**         | Automatic two-way trusts           | Configurable trust relationships    |
| **Management**     | Shared enterprise control          | Independent control per tree        |


### Practical Example
- **Scenario 1:**  
  A multinational company creates a tree:
  - Root Domain: `company.local`
  - Subdomains: `us.company.local`, `uk.company.local`

- **Scenario 2:**  
  After acquiring another company:
  - Trees: `company.local` and `newcompany.com`
  - Combined into a forest for unified network management.

- **Resource Sharing:**  
  Trust relationships allow specific resource sharing between domains as needed while maintaining security and management boundaries.
