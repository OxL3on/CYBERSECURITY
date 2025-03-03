# REMnux: Getting Started



### REMnux Intro

**Main Idea:** REMnux VM is a ready-to-go Linux setup for safely checking out sketchy software.

**What It’s About:**  
- Analyzing bad software (malware) is tricky, especially during a security mess.  
- REMnux is a special Linux VM packed with tools like Volatility, YARA, and Wireshark.  
- It’s like a sandbox lab—keeps your main system safe while you poke at malware.

**Why It’s Cool:**  
- No setup hassle—tools are already there for accurate analysis.

**Remembering Tip:** Think of REMnux as your “malware detective kit”—pre-loaded with gadgets, safe in its own little crime lab!

---


### File Analysis with REMnux

**Main Idea:** Use `oledump.py` on REMnux VM to peek inside a shady Excel file without running it.

**What’s Happening:**  
- Tool: `oledump.py` checks OLE2 files (like Excel) for hidden stuff.  
- Example: On REMnux VM, go to `/home/ubuntu/Desktop/tasks/agenttesla/` and run:  
  ```bash
  oledump.py agenttesla.xlsm
  ```
- Output shows streams (e.g., `A4: M 688 'VBA/ThisWorkbook'`)—`M` means a Macro’s hiding there!

**Digging Deeper:**  
- Run: `oledump.py agenttesla.xlsm -s 4 --vbadecompress`  
  - `-s 4` picks stream A4, `--vbadecompress` makes the Macro readable.  
- Result: A sneaky PowerShell script (`Sqtnew`) downloads and runs `Doc-3737122pdf.exe` from `http://193.203.203.67/rt/`.

**Cleaning It Up:**  
- Copy `Sqtnew` to CyberChef, use “Find/Replace” twice:  
  - Replace `*` with nothing.  
  - Replace `^` with nothing.  
- Now it’s clear: PowerShell hides, bypasses rules, grabs an .exe, and runs it.

**Why It’s Bad:**  
- When `agenttesla.xlsm` opens, this Macro sneaks in malware—tricky and quiet!

**Remembering Tip:** Think of `oledump` as a “file X-ray”—spots a Macro “bomb” that CyberChef defuses to reveal the plan!

---


### Fake Network with INetSim

**Main Idea:** Use INetSim on REMnux VM to fake a network and watch malware’s moves.

**Setup on REMnux:**  
- Check your IP: `ifconfig` (e.g., `MACHINE_IP`).  
- Edit config: `sudo nano /etc/inetsim/inetsim.conf`  
  - Change `#dns_default_ip 0.0.0.0` to `dns_default_ip MACHINE_IP`.  
  - Save (Ctrl+O, Enter, Ctrl+X).  
- Start it: `sudo inetsim` (look for “Simulation running”).

**Test on AttackBox:**  
- Open browser, go to `https://MACHINE_IP` (ignore security warning).  
- Mimic malware: Download fake files with:  
  ```bash
  sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate
  ```
  - Try another: `sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate`.  
- Files are fake—`second_payload.ps1` just loops to INetSim’s page.

**Check Results:**  
- Stop INetSim on REMnux, check report:  
  ```bash
  sudo cat /var/log/inetsim/report/report.2594.txt
  ```
- Shows fake connections (e.g., HTTPS GETs to `MACHINE_IP`).

**Why It’s Cool:** Tricks malware into showing its network tricks safely.

**Remembering Tip:** Think of INetSim as a “movie set”—fakes a network town for malware to act out its scenes!

---


### Memory Preprocessing with REMnux

**Main Idea:** Prep memory evidence fast using Volatility and Strings on REMnux VM.

**Volatility Basics:**  
- Tool: Volatility 3 (on REMnux) digs into memory files (e.g., `wcry.mem`).  
- Go to: `/home/ubuntu/Desktop/tasks/Wcry_memory_image/`.  
- Plugins to try (each takes 2-3 mins):  
  - `windows.pstree.PsTree`: Shows process tree.  
  - `windows.pslist.PsList`: Lists active processes.  
  - `windows.cmdline.CmdLine`: Grabs command args.  
  - `windows.filescan.FileScan`: Finds files.  
  - `windows.dlllist.DllList`: Lists loaded DLLs.  
  - `windows.psscan.PsScan`: Scans for processes.  
  - `windows.malfind.Malfind`: Spots sneaky code.  
- Example: `vol3 -f wcry.mem windows.pstree.PsTree`.

**Bulk Preprocessing:**  
- Run all at once:  
  ```bash
  for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
  ```
- Saves each result to a `.txt` file (e.g., `wcry.windows.pstree.PsTree.txt`).

**Strings Preprocessing:**  
- Extract text from `wcry.mem`:  
  ```bash
  strings wcry.mem > wcry.strings.ascii.txt
  strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
  strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
  ```
- Makes 3 files with ASCII and Unicode strings.

**Why It’s Handy:** Saves time—files are ready for analysts to dig into later.

**Remembering Tip:** Think of Volatility as a “memory chef”—chopping up evidence into bite-sized files with a quick loop recipe!

