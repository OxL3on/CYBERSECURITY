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


