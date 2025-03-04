# Security Principles


### CIA

**Main Idea:** Security means keeping data safe using the CIA triangle: Confidentiality, Integrity, Availability.

**CIA Explained:**  
- **Confidentiality:** Only the right people see it (e.g., your credit card stays secret online).  
- **Integrity:** Data stays true, no sneaky changes (e.g., shipping address isn’t swapped).  
- **Availability:** System’s up when you need it (e.g., online store works for shopping).  

**Example:**  
- Shopping online: Card info’s hidden (confidentiality), order’s unchanged (integrity), site’s online (availability).  

**Beyond CIA:**  
- **Authenticity:** It’s really from who it says (e.g., order’s from a real customer).  
- **Nonrepudiation:** They can’t deny sending it (e.g., customer can’t say “I didn’t order 1000 cars!”).  

**Parkerian Hexad Bonus:**  
- **Utility:** Data’s useful (e.g., encrypted laptop’s no good without the key).  
- **Possession:** You keep control (e.g., ransomware locks you out—lost possession).  

**Remembering Tip:** Think of CIA as a “security shield”—keeps secrets in, fakes out, and doors open, with extras like “proof” and “power”!

---


### DAD Triad

**Main Idea:** DAD (Disclosure, Alteration, Destruction) is the flip side of CIA—ways security gets attacked.

**DAD Explained:**  
- **Disclosure:** Secrets leak out (breaks confidentiality, e.g., medical records go public).  
- **Alteration:** Data gets messed up (breaks integrity, e.g., patient records changed = wrong treatment).  
- **Destruction/Denial:** System’s knocked out (breaks availability, e.g., hospital database down = chaos).  

**Example:**  
- Hospital hack: Records stolen (disclosure), treatments altered (alteration), system crashed (denial)—big trouble!

**Why It Matters:**  
- Stopping DAD keeps CIA strong.  
- Too much focus on one (like locking down confidentiality) can weaken another (like availability)—balance is key.

**Remembering Tip:** Think of DAD as the “bad guy trio”—spilling secrets, twisting truth, and smashing access!

---


### Security Models

**Main Idea:** Security models like CIA (Confidentiality, Integrity, Availability) help build safe systems.

**Key Models:**  
1. **Bell-LaPadula (Confidentiality):**  
   - Rules: “No read up” (low can’t see high secrets), “No write down” (high can’t leak to low).  
   - Example: Spy can’t read Top Secret files but can send reports up.  
   - Limit: Doesn’t handle file-sharing well.  

2. **Biba (Integrity):**  
   - Rules: “No read down” (don’t trust lower data), “No write up” (low can’t mess high data).  
   - Example: Boss reads worker’s report, but worker can’t edit boss’s files.  
   - Limit: Misses insider threats.  

3. **Clark-Wilson (Integrity):**  
   - Uses: CDIs (key data to protect), UDIs (other data), TPs (safe operations), IVPs (checks).  
   - Example: Bank locks account totals (CDI), checks math (IVP) after updates (TP).  

**Why They Matter:** Each fixes a CIA piece—pick the right one for your goal.

**Remembering Tip:** Think of models as “security recipes”—Bell-LaPadula hides secrets, Biba keeps truth clean, Clark-Wilson double-checks the math!

---


### ISO/IEC 19249

**Main Idea:** ISO/IEC 19249 gives rules to build secure systems with architecture and design tricks.

**5 Architectural Principles:**  
- **Domain Separation:** Group stuff by security level (e.g., OS kernel vs. apps).  
- **Layering:** Stack layers with rules (e.g., OSI model in networking).  
- **Encapsulation:** Hide details, use safe methods (e.g., clock’s `increment()`).  
- **Redundancy:** Backup for uptime and truth (e.g., RAID 5 keeps data safe).  
- **Virtualization:** Share hardware, sandbox bad stuff (e.g., cloud VMs).  

**5 Design Principles:**  
1. **Least Privilege:** Only give what’s needed (e.g., read-only for docs).  
2. **Attack Surface Minimisation:** Cut weak spots (e.g., disable extra Linux services).  
3. **Centralized Parameter Validation:** Check inputs in one spot (e.g., one validation library).  
4. **Centralized General Security Services:** One hub for security (e.g., central login server).  ISO/IEC 19249

The International Organization for Standardization (ISO) and the International Electrotechnical Commission (IEC) have created the ISO/IEC 19249. In this task, we will brush briefly upon ISO/IEC 19249:2017 Information technology - Security techniques - Catalogue of architectural and design principles for secure products, systems and applications. The purpose is to have a better idea of what international organizations would teach regarding security principles.

ISO/IEC 19249 lists five architectural principles:

    Domain Separation: Every set of related components is grouped as a single entity; components can be applications, data, or other resources. Each entity will have its own domain and be assigned a common set of security attributes. For example, consider the x86 processor privilege levels: the operating system kernel can run in ring 0 (the most privileged level). In contrast, user-mode applications can run in ring 3 (the least privileged level). Domain separation is included in the Goguen-Meseguer Model.
    Layering: When a system is structured into many abstract levels or layers, it becomes possible to impose security policies at different levels; moreover, it would be feasible to validate the operation. Let’s consider the OSI (Open Systems Interconnection) model with its seven layers in networking. Each layer in the OSI model provides specific services to the layer above it. This layering makes it possible to impose security policies and easily validate that the system is working as intended. Another example from the programming world is disk operations; a programmer usually uses the disk read and write functions provided by the chosen high-level programming language. The programming language hides the low-level system calls and presents them as more user-friendly methods. Layering relates to Defence in Depth.
    Encapsulation: In object-oriented programming (OOP), we hide low-level implementations and prevent direct manipulation of the data in an object by providing specific methods for that purpose. For example, if you have a clock object, you would provide a method increment() instead of giving the user direct access to the seconds variable. The aim is to prevent invalid values for your variables. Similarly, in larger systems, you would use (or even design) a proper Application Programming Interface (API) that your application would use to access the database.
    Redundancy: This principle ensures availability and integrity. There are many examples related to redundancy. Consider the case of a hardware server with two built-in power supplies: if one power supply fails, the system continues to function. Consider a RAID 5 configuration with three drives: if one drive fails, data remains available using the remaining two drives. Moreover, if data is improperly changed on one of the disks, it would be detected via the parity, ensuring the data’s integrity.
    Virtualization: With the advent of cloud services, virtualization has become more common and popular. The concept of virtualization is sharing a single set of hardware among multiple operating systems. Virtualization provides sandboxing capabilities that improve security boundaries, secure detonation, and observance of malicious programs.

ISO/IEC 19249 teaches five design principles:

    Least Privilege: You can also phrase it informally as “need-to basis” or “need-to-know basis” as you answer the question, “who can access what?” The principle of least privilege teaches that you should provide the least amount of permissions for someone to carry out their task and nothing more. For example, if a user needs to be able to view a document, you should give them read rights without write rights.
    Attack Surface Minimisation: Every system has vulnerabilities that an attacker might use to compromise a system. Some vulnerabilities are known, while others are yet to be discovered. These vulnerabilities represent risks that we should aim to minimize. For example, in one of the steps to harden a Linux system, we would disable any service we don’t need.
    Centralized Parameter Validation: Many threats are due to the system receiving input, especially from users. Invalid inputs can be used to exploit vulnerabilities in the system, such as denial of service and remote code execution. Therefore, parameter validation is a necessary step to ensure the correct system state. Considering the number of parameters a system handles, the validation of the parameters should be centralized within one library or system.
    Centralized General Security Services: As a security principle, we should aim to centralize all security services. For example, we would create a centralized server for authentication. Of course, you might take proper measures to ensure availability and prevent creating a single point of failure.
    Preparing for Error and Exception Handling: Whenever we build a system, we should take into account that errors and exceptions do and will occur. For instance, in a shopping application, a customer might try to place an order for an out-of-stock item. A database might get overloaded and stop responding to a web application. This principle teaches that the systems should be designed to fail safe; for example, if a firewall crashes, it should block all traffic instead of allowing all traffic. Moreover, we should be careful that error messages don’t leak information that we consider confidential, such as dumping memory content that contains information related to other customers.

In the following questions, refer to the ISO/IEC 19249 five design principles above. Answer with a number between 1 and 5, depending on the number of the design principle.
5. **Preparing for Error Handling:** Plan for fails (e.g., firewall blocks all if it crashes).  

**Example:** Online shop—only staff see orders (1), no unused features (2), one input checker (3), single login system (4), out-of-stock error won’t spill secrets (5).

**Remembering Tip:** Think of 19249 as a “security blueprint”—architecture builds the house, design locks the doors!

---



### Trust but Verify vs. Zero Trust


**Main Idea:** Two ways to handle trust in security—check it or ditch it.

**Trust but Verify:**  
- Trust first, but double-check (e.g., let a user in, then log their clicks).  
- Needs tools like proxies or IDS to watch stuff automatically.  
- Example: Boss trusts you but peeks at your web history.

**Zero Trust:**  
- No trust ever—everything’s a suspect until proven safe (e.g., no free pass for company laptops).  
- Always authenticate and limit access, even inside the network.  
- Microsegmentation: Tiny network zones, each locked tight.  
- Example: Every door needs a key, even in your own house.

**Why It Matters:**  
- Trust but Verify is lighter but misses sneaky insiders.  
- Zero Trust locks down more but can slow things if overdone.

**Remembering Tip:** Think of Trust but Verify as a “friendly handshake with a spy cam,” and Zero Trust as “no hugs, just ID checks”!

---


