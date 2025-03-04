# FlareVM: Arsenal of Tools


### FlareVM Intro

**Main Idea:** FlareVM is a toolbox for cracking digital puzzles like malware.

**What It Is:**  
- Full name: Forensics, Logic Analysis, and Reverse Engineering VM.  
- Made by FireEye’s FLARE Team.  
- Packed with tools for reverse engineers, malware analysts, and forensic pros.

**Why It’s Cool:**  
- Helps figure out what sneaky software does without breaking a sweat.

**Remembering Tip:** Think of FlareVM as a “digital detective kit”—unlocks secrets in executables like a pro!

---



### FlareVM Tools

**Main Idea:** FlareVM’s got a big toolbox for cracking malware and digital mysteries.

**Key Tools by Job:**  
- **Reverse Engineering & Debugging:** Puzzle out code.  
  - Ghidra, x64dbg, OllyDbg—break down binaries.  
- **Disassemblers & Decompilers:** Read malware’s guts.  
  - CFF Explorer, Hopper—turn code into plain text.  
- **Static & Dynamic Analysis:** Check code still or running.  
  - Process Hacker, PEview—watch processes or peek at files.  
- **Forensics & Incident Response:** Hunt evidence.  
  - Volatility, FTK Imager—dig through memory or disks.  
- **Network Analysis:** Spy on traffic.  
  - Wireshark, Nmap—sniff packets or map networks.  
- **File Analysis:** Peek inside files.  
  - FileInsight, HxD—edit or view binary stuff.  
- **Scripting & Automation:** Speed things up.  
  - Python, PowerShell Empire—automate tasks.  
- **Sysinternals Suite:** Windows deep dive.  
  - Process Explorer, Autoruns—track what’s running.

**Why It’s Cool:** One VM, tons of tools for any job—pick what fits!

**Remembering Tip:** Think of FlareVM as a “cyber tool belt”—grab the right gadget for the malware mess!

---


### FlareVM Investigation Tools

**Main Idea:** FlareVM has key tools to kick off malware investigations.

**Top Tools:**  
- **Procmon:** Tracks system activity (e.g., lsass.exe reading files—watch for odd stuff).  
- **Process Explorer:** Shows process family trees (e.g., CFF Explorer’s parent).  
- **HxD:** Hex editor for file peeking (e.g., `4D 5A` = executable start).  
- **Wireshark:** Sniffs network traffic (e.g., TLSv1.2 packets).  
- **CFF Explorer:** Checks file details (e.g., cryptominer.bin’s hashes).  
- **PEStudio:** Static file analysis (e.g., PsExec.exe’s entropy hints at danger).  
- **FLOSS:** Pulls hidden strings (e.g., 189 static strings from cobaltstrike.exe).

**Example:**  
- Run `floss cobaltstrike.exe`—grabs strings like URLs or keys, but no decoded ones means sneaky hiding.

**Why They Rock:** Spot malware tricks fast—some watch live, others dig static.

**Remembering Tip:** Think of these tools as “cyber magnifying glasses”—each zooms in on a different clue (processes, files, networks)!

---


### Analyzing Malware with FlareVM

**Main Idea:** Dive into suspicious files using FlareVM tools to spot their tricks.

**PEStudio on `windows.exe`:**  
- Open `C:\Users\Administrator\Desktop\Sample\windows.exe` in PEStudio.  
- Key Finds:  
  - Hashes: MD5 `9FDD4767DE5AEC8E577C1916ECC3E1D6`—check VirusTotal.  
  - Fake REGEDIT label, Russian text in metadata—suspicious!  
  - No rich header = packed/obfuscated.  
  - APIs: `set_UseShellExecute` (spawns stuff), `RijndaelManaged` (AES encryption—maybe ransomware).

**FLOSS on `windows.exe`:**  
- Run: `FLOSS.exe .\windows.exe > windows.txt` in PowerShell.  
- Check `windows.txt`—same APIs as PEStudio, no decoded strings (hidden tricks).

**Process Explorer & Procmon on `cobaltstrike.exe`:**  
- Run `cobaltstrike.exe`, open Process Explorer.  
  - See it under Explorer.exe (PID 4756), check TCP/IP tab—network connections!  
- Rerun, use Procmon: Filter for “cobalt” (Ctrl+L).  
  - Confirms connection to IP `47.120.46.210`—possible C2 server.

**Why It’s Cool:** Static (PEStudio, FLOSS) gives clues, dynamic (Procmon, Process Explorer) catches action.

**Remembering Tip:** Think of these tools as “malware detectives”—PEStudio and FLOSS read the file’s diary, Process Explorer and Procmon spy on its phone calls!
