# CAPA: The Basics



### CAPA Introduction

**Main Idea:** CAPA is a tool for static analysis of software to spot what it can do without running it.

**What It Does:**  
- Checks files like PE, ELF, .NET, or shellcode.  
- Uses rules to find capabilities (e.g., network use, file changes, process tricks).  
- Made by FireEye Mandiant for easy analysis.

**Why It’s Cool:**  
- No need to risk your machine—works without a sandbox.  
- Turns expert reverse engineering into an auto-tool.  
- Great for malware analysis and threat hunting.

**Remembering Trick:** Think of CAPA as a “crystal ball” for code—peeking at what a program might do without letting it loose!

---



### How CAPA Works

**Main Idea:** CAPA scans binaries to spot what they can do, super easy to run.

**How to Use:**  
1. Open PowerShell, go to `C:\Users\Administrator\Desktop\capa`.  
2. Run: `capa.exe .\filename` (e.g., `cryptbot.bin`).  
3. Wait for results (takes minutes) or check pre-run output (e.g., `Get-Content cryptbot.txt`).

**Options:**  
- `-h`: See help.  
- `-v`: More details.  
- `-vv`: Super detailed (slower).

**What You Get:**  
- File info (MD5, OS, format).  
- ATT&CK tactics (e.g., Defense Evasion).  
- Behaviors (e.g., XOR encoding, file writing).  
- Capabilities (e.g., “create process,” “schedule task”).

**Why It’s Handy:** Quick peek at a file’s tricks without running it.

**Remembering Trick:** Think of CAPA as a “binoculars” for binaries—zoom in (run it), spot tricks (results), no danger!

---


### CAPA Results I

**Main Idea:** CAPA’s results break down a file’s basics, attack moves, and malware type.

**1. General Info:**  
- Shows file hashes (MD5, SHA1, SHA256), analysis type (static), OS (Windows), format (PE), architecture (i386), and file path.  
- *Example:* `cryptbot.bin` = Windows PE, 32-bit.

**2. MITRE ATT&CK:**  
- Maps file tricks to attack tactics/techniques (e.g., Defense Evasion: Obfuscated Files [T1027]).  
- Format: Tactic::Technique::[ID] (or Sub-Technique::[ID.Sub-ID]).  
- *Examples:* Hides data (T1027), runs PowerShell (T1059.001), schedules tasks (T1053.005).  
- *Why:* Links file behavior to hacker playbook for faster response.

**3. MAEC (Malware Attributes):**  
- Tags malware type (e.g., “launcher” for `cryptbot.bin`).  
- **Launcher:** Triggers actions (drops payloads, calls C2, persists).  
- **Downloader:** Grabs more files (updates, configs).  

**Remembering Trick:** Think of CAPA as a “file profiler”—General Info is the ID card, MITRE is the rap sheet, MAEC is the nickname (launcher/downloader)!

---



### CAPA Results II

**Main Idea:** MBC in CAPA lists what malware can do, linking to ATT&CK but with extra detail.

**Key Parts:**  
1. **Objective:** Big goals (e.g., Defense Evasion, Data).  
   - *Examples:* Anti-Static Analysis (hides from tools), Execution (runs code).  
2. **Micro-Objective:** Smaller actions (e.g., Process, Memory).  
   - *Examples:* PROCESS (creates processes), DATA (encodes stuff).  
3. **Behavior:** What it does (e.g., Encode Data, HTTP Communication).  
4. **Micro-Behavior:** Low-level moves (e.g., Allocate Memory, Check String).  
5. **Methods:** How it does it (e.g., Base64, XOR).  

**MBC Format:**  
- `OBJECTIVE::Behavior::Method [ID]` (e.g., `DATA::Encode Data::Base64 [C0026.001]`).  
- *Explanation:* This file encodes data with Base64.

**Sample Recap:**  
- `DATA::Encode Data::Base64 [C0026.001]` = File uses Base64 to hide data.

**Why It Matters:** Helps analysts tag and understand malware tricks fast.

**Remembering Trick:** Think of MBC as a “malware menu”—Objectives are cuisines, Behaviors are dishes, Methods are spices, and IDs are order numbers!

---


### CAPA Results III

**Main Idea:** CAPA’s namespaces group what a file can do into categories.

**Format:** `Capability::Top-Level Namespace/Namespace`  
- *Example:* `reference anti-VM strings::anti-analysis/anti-vm/vm-detection`

**Namespaces Explained:**  
- **Top-Level Namespace (TLN):** Big category (e.g., `anti-analysis`).  
- **Namespace:** Sub-group (e.g., `anti-vm/vm-detection`).  
- *Examples:*  
  - `anti-analysis/anti-vm/vm-detection`: Spots VM checks (e.g., VirtualBox strings).  
  - `communication/http`: Flags HTTP use (e.g., User-Agent strings).  
  - `host-interaction/file-system/write`: Notes file writing (e.g., 5 matches in `cryptbot.bin`).  
  - `persistence/scheduled-tasks`: Marks task scheduling (e.g., via `schtasks`).

**Key TLNs:**  
- `anti-analysis`: Hides from tools (e.g., VM detection, obfuscation).  
- `communication`: Talks to networks (e.g., HTTP).  
- `data-manipulation`: Changes data (e.g., Base64, XOR).  
- `host-interaction`: Messes with the system (e.g., files, processes).  
- `persistence`: Stays sneaky (e.g., scheduled tasks).

**Why It Matters:** Organizes file tricks for easy understanding.

**Remembering Trick:** Think of namespaces as a “file cabinet”—TLN is the drawer (e.g., `anti-analysis`), Namespace is the folder (e.g., `vm-detection`), holding rule papers!

---


### CAPA Results IV

**Main Idea:** Capabilities show what a file can do, tied to rules in namespaces.

**How It Works:**  
- **Capability:** The action (e.g., `reference Base64 string`).  
- Matches a rule file (e.g., `reference-base64-string.yml`).  
- Lives under a **Top-Level Namespace (TLN)** (e.g., `data-manipulation`) and **Namespace** (e.g., `encoding/base64`).  

**Examples:**  
- `reference anti-VM strings` → `anti-analysis/anti-vm/vm-detection`  
  - Checks for VM clues (rule: `reference-anti-vm-strings.yml`).  
- `schedule task via schtasks` → `persistence/scheduled-tasks`  
  - Sets up persistence (rule: `schedule-task-via-schtasks.yml`).  
- `reference Base64 string` → `data-manipulation/encoding/base64`  
  - Uses Base64 encoding (rule: `reference-base64-string.yml`).  

**Note:**  
- Capability names match rule files (spaces become dashes).  
- Some rules (e.g., `reference cryptocurrency strings`) sit in `nursery` (unpolished rules), not their expected TLN.

**Recap Sample:**  
- `reference Base64 string::data-manipulation/encoding/base64` = File can encode data with Base64.

**Remembering Trick:** Think of Capability as a “superpower” name, rule file as its “spellbook,” and Namespace as the “school” it learned from!

---


### More CAPA Fun

**Main Idea:** Use `-vv` and CAPA Web Explorer to dig deep into why rules trigger.

**How to Get More Detail:**  
- Run: `capa.exe -vv .\cryptbot.bin` (very verbose, takes time).  
- Save as JSON: `capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json`.  
- Pre-made file: `cryptbot_vv.json` in `C:\Users\Administrator\Desktop\capa`.

**CAPA Web Explorer:**  
- Open in Chrome (online or offline: `capa_web_explorer_offline.html`).  
- Upload `cryptbot_vv.json` via “Upload from local.”  
- See detailed, easy-to-read results.

**Examples:**  
1. **Anti-VM Strings (VMWare):**  
   - Rule: `reference-anti-vm-strings-targeting-vmware.yml`.  
   - Trigger: Matches string `/VMWare/i` (case-insensitive regex).  
2. **Schedule Task via schtasks:**  
   - Rule: `schedule-task-via-schtasks.yml`.  
   - Trigger: Matches strings `/schtasks/i` and `/\/create /i`.

**Cool Feature:**  
- **Global Search Box:** Filter tons of data fast.

**Why It’s Fun:** Shows exactly what matched (e.g., strings like “VMWare” or “schtasks”).

**Remembering Trick:** Think of `-vv` as “very vocal” CAPA spilling secrets, and Web Explorer as a “magnifying glass” zooming into the clues!

