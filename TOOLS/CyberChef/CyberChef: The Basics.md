# CyberChef: The Basics


### CyberChef Introduction

**Main Idea:** CyberChef is a web-based “toolbox” for cyber tasks, making data fiddling easy.

**What It Does:**  
- Handles simple stuff like XOR or Base64 encoding.  
- Tackles tricky tasks like AES encryption or RSA decryption.  
- Uses “recipes”—a list of steps done in order.

**Why It’s Handy:**  
- Runs in your browser, no install needed.  
- Like a Swiss Army knife for data tweaks.

**Remembering Trick:** Think of CyberChef as a “data chef”—whipping up recipes to cook (encode) or uncook (decode) cyber ingredients!

---


### Navigating CyberChef Interface

**Main Idea:** CyberChef’s layout has four key areas to work with data easily.

**The Four Areas:**  
1. **Operations:** Toolbox of actions (e.g., Base64, ROT13).  
   - Search or hover for examples like “THREATS” from Morse “- .... .-. . .- - ...”.  
2. **Recipe:** Where you pick and tweak operations in order.  
   - Features: Save, load, or clear recipes. Hit “BAKE!” to run (or use Auto Bake).  
3. **Input:** Space to add text or files (type, paste, drag).  
   - Options: New tabs, upload files/folders, clear all.  
4. **Output:** Shows results after baking.  
   - Options: Save to file, copy, replace input, maximize view.

**Why It’s Cool:** Simple setup to encode, decode, or transform data fast.

**Remembering Trick:** Think of CyberChef as a kitchen—Operations are ingredients, Recipe is your cooking steps, Input is raw food, Output is the tasty dish!

---


### Before Anything Else

**Main Idea:** CyberChef has a 4-step thought process to tackle data tasks.

**The Steps:**  
1. **Set a Goal:** Decide what you want (e.g., “Decode this weird string from an investigation”).  
2. **Add Data:** Put your stuff in the input area (e.g., paste that gibberish string).  
3. **Pick Operations:** Choose tools to try (e.g., Base64 or ROT13 if it’s encrypted).  
   - Might take research if you’re unsure.  
4. **Check Output:** See if it worked (e.g., “Did I get a hidden message?”).  
   - If not, restart from step 1.

**Why It Helps:** Keeps you focused and systematic.

**Remembering Trick:** Think of it as a treasure hunt—set your prize (goal), grab the map (data), pick your tools (operations), and check if you found gold (output)!

---


### Practice with CyberChef

**Main Idea:** Get good at CyberChef by practicing key operation categories.

**Extractor Tools:**  
- **Extract IPs:** Grabs IPv4/6 addresses from text.  
- **Extract URLs:** Pulls web links (e.g., `http://tryhackme.com`).  
- **Extract Emails:** Finds emails (e.g., `user@tryhackme.com`).  

**Date/Time Tools:**  
- **From UNIX Timestamp:** Turns seconds since 1970 (e.g., 1725654622) into a date (e.g., "Fri Sep 6 2024").  
- **To UNIX Timestamp:** Converts a date back to seconds.  

**Data Format Tools:**  
- **From Base64:** Decodes to text (e.g., `VEhN` → "THM").  
- **URL Decode:** Unpacks encoded URLs (e.g., `https%3A%2F%2Ftryhackme.com` → `https://tryhackme.com`).  
- **From Base85:** Decodes denser text (e.g., `BOu!rD]j7BEbo7` → "hello world").  
- **From Base58:** Decodes readable text (e.g., `AXLU7qR` → "Thm58").  
- **To Base62:** Encodes short strings (e.g., "Thm62" → `6NiRkOY`).  

**Base64 Example (THM):**  
- "THM" → Binary (01010100 01001000 01001101) → Split (6-bit: 010101 000100 100001 001101) → Decimal (21 4 33 13) → Base64 (VEhN).  

**Why Practice:** Knowing these categories speeds up your work.

**Remembering Trick:** Think of CyberChef as a data “detective”—Extractors find clues, Date/Time cracks timelines, Data Format decodes secret messages!

