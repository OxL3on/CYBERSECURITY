# Active Directory Basics
[LINK](https://tryhackme.com/room/winadbasics)


- **Windows Domain** — a group of users/computers under centralized administration; primary target for lateral movement and privilege escalation
- **Active Directory (AD)** — centralized repository storing all user, computer, and policy objects; *the* crown jewel in Windows environments
- **Domain Controller (DC)** — the server running AD services; highest-value target in any Windows network — own the DC, own the domain
- **Centralized identity management** — credentials validated by AD, not local machines; enables pass-the-hash, Kerberoasting, and credential replay attacks
- **Domain credentials** — valid across *all* machines in the domain; one compromised account can mean network-wide access
- **Security policies via AD** — Group Policy Objects (GPOs) control privileges, restrictions, and configurations across the network; attackers abuse GPO misconfigurations for persistence and privilege escalation
- **Administrative privileges** — centrally managed; understanding who has local vs. domain admin is critical for attack paths

<br>

**AD Object Types**

- **AD DS (Active Directory Domain Services)** — the core catalogue of every object on the network; your primary enumeration target
- **Security Principals** — objects that can authenticate and act on resources: **Users**, **Machines**, and **Security Groups** — these are what you're hunting to compromise or abuse
- **Service Accounts** — user objects running services (IIS, MSSQL, etc.); high-value targets because they often have elevated privileges and weak/static passwords → **Kerberoasting**
- **Machine Accounts** (`DC01$` format) — local admin on their own machine; 120-char auto-rotated passwords, but if you can dump one, you can impersonate that computer on the domain


**Default High-Value Groups**

| Group | Why Offensively Interesting |
|---|---|
| **Domain Admins** | Full domain control — end goal |
| **Server Operators** | Can administer DCs — near DA-level |
| **Backup Operators** | Can read *any* file regardless of ACLs → dump NTDS.dit |
| **Account Operators** | Can create/modify accounts → persistence |


**Organizational Units (OUs)**

- Container for users/computers with **GPOs applied** — misconfigured GPO permissions = privilege escalation
- Structure mirrors org chart (IT, Sales, HR) → useful for **OSINT and targeting** during recon
- Tools like **BloodHound** map OU → GPO → user relationships


**Default Containers to Know**

- `Computers` — where unmanaged machines land by default; often overlooked, sometimes misconfigured
- `Domain Controllers` — know exactly which machines are DCs immediately
- `Users` — default domain-wide users and groups live here


**OUs vs Security Groups**

- **OUs** → GPO application (abuse for policy-based attacks, persistence)
- **Security Groups** → resource permissions (abuse for lateral movement, accessing shares, printers, etc.)
- A user can be in **many groups** but only **one OU** — important when mapping attack paths in BloodHound


<br>


**Delegation**

- **Delegation of Control** — granting a non-admin user specific privileges over an OU (e.g., password resets, account unlocks); commonly **misconfigured** and abused during privilege escalation



**OU Protection Bypass**

- OUs have **accidental deletion protection** by default — requires enabling **Advanced Features** in ADUC to remove

**PowerShell AD Commands**

```powershell
# Force reset another user's password
Set-ADAccountPassword <user> -Reset -NewPassword (Read-Host -AsSecureString)

# Force password change at next logon (cover tracks / maintain access)
Set-ADUser -ChangePasswordAtLogon $true -Identity <user>
```

These work **without ADUC GUI access** — key for low-priv shells

**LDAP Distinguished Name (DN) Format**

From the verbose output:
```
CN=Sophie, OU=Sales, OU=THM, DC=thm, DC=local
```
- **CN** = Common Name (object)
- **OU** = Organizational Unit (nested, inner → outer)
- **DC** = Domain Component (domain = `thm.local`)

<br>


**Machine Segregation**

| Tier | Device Type | Sensitivity |
|---|---|---|
| Tier 2 | Workstations | Lowest — user entry point |
| Tier 1 | Servers | Medium — services, data |
| Tier 0 | Domain Controllers | Highest — hashed passwords for **every** account |


**Domain Controllers**

- DCs store **NTDS.dit** — the AD database containing hashed passwords for all domain users
- Owning a DC = owning the entire domain
- Attack paths that lead here: DCSync, Golden Ticket, NTDS.dit extraction


**Workstations**

- Where users log in daily → **phishing, drive-by, credential harvesting** land here first
- Should never have privileged users logged in (but often do) → if a DA logs into a workstation, their credentials are **exposed in memory** → Mimikatz
- This is the start of most real-world attack chains


**Servers**

- Host services (web, SQL, file shares) → exploitation leads to **service account compromise**
- Service accounts are often over-privileged → Kerberoasting targets
- Pivot point between workstations and DCs

<br>


**GPO Basics**
- **GPO** = collection of settings applied to an OU (and all sub-OUs by default)
- **Scope:** parent OU GPO → inherited by all child OUs
- **Two config types:** Computer Configuration / User Configuration


**SYSVOL**
- GPOs distributed via `\\domain\SYSVOL` share on the DC
- **All domain users can read it** by default
- Common finding: **passwords/scripts stored in SYSVOL** → plaintext creds
- Path: `C:\Windows\SYSVOL\sysvol\`

```powershell
# Force GPO sync (useful post-exploitation)
gpupdate /force
```


**Offensive GPO Abuse**
If you have **write access to a GPO** (misconfigured ACL) → you can:
- Add yourself to Domain Admins
- Deploy a malicious script to all machines in linked OU
- Create backdoor accounts domain-wide

Tool: **SharpGPOAbuse**


**Recon Value**
Reading GPOs tells you:
- Password policy (min length, lockout threshold → guides brute force)
- What's blocked where (AV, control panel, PowerShell restrictions)
- Which OUs have relaxed policies → softer targets

<br>

**Kerberos (default, modern)**

Key components:
- **KDC** — runs on DC, issues all tickets
- **TGT** — encrypted with `krbtgt` hash; proves identity, used to request service tickets
- **TGS** — ticket for a specific service, encrypted with **Service Owner's hash**
- **SPN** — identifier for a service (`http/webserver.thm.local`)

Attack surface:
| Attack | How |
|---|---|
| **Kerberoasting** | Request TGS for any SPN → crack Service Owner hash offline |
| **AS-REP Roasting** | User has pre-auth disabled → grab encrypted TGT → crack offline |
| **Golden Ticket** | Forge TGT using `krbtgt` hash → unlimited domain access |
| **Silver Ticket** | Forge TGS using Service Owner hash → access specific service |
| **Pass-the-Ticket** | Steal TGT from memory → reuse without knowing password |


**NetNTLM (legacy, still everywhere)**

Challenge-response — hash never sent directly, but:
| Attack | How |
|---|---|
| **NTLM Relay** | Intercept challenge-response → relay to another service |
| **Responder** | Force auth to your machine → capture NetNTLM hash → crack or relay |
| **Pass-the-Hash** | Use NTLM hash directly without cracking |


**Key Fact**
- Local accounts → server verifies against local **SAM** (no DC involved) → useful for lateral movement with local admin hashes

<br>


**Tree vs Forest**
- **Tree** — multiple domains sharing same namespace (`thm.local`, `uk.thm.local`)
- **Forest** — multiple trees with different namespaces (`thm.local` + `mht.local`)


**Key Groups**
- **Domain Admins** — controls single domain
- **Enterprise Admins** — controls ALL domains in the forest → highest privilege target


**Trust Relationships**
- **One-way trust:** AAA trusts BBB → BBB users can access AAA resources
- **Two-way trust:** default when joining trees/forests → mutual access
- Trust ≠ full access — just opens the *possibility* of cross-domain auth

<br>

# Intro to AD Authentication
[LINK](https://tryhackme.com/room/introtoactivedirectoryauthentication)


**Authentication vs Authorisation**
- **AuthN** = prove identity ("who are you?")
- **AuthZ** = determine access ("what can you do?") → checked via group memberships + ACLs

- 
**Authentication Material**
| Type | Offensive Use |
|---|---|
| Password | Brute force, spraying |
| Hash | Pass-the-Hash, cracking |
| Certificate | Pass-the-Certificate, ADCS attacks (ESC1-8) |
| Ticket (TGT/TGS) | Pass-the-Ticket, Golden/Silver Ticket |


**Two Core Protocols (everything else builds on these)**
- **NetNTLM** → challenge-response → relay/capture attacks
- **Kerberos** → ticket-based → roasting/forging attacks

<br>


**NTLM Versions**
- **NTLMv1** — critically weak, crack almost instantly
- **NTLMv2** — stronger but still unsalted → crackable, still relayable


**Why It's Still Everywhere**
- Fallback when Kerberos fails
- Used when accessing by **IP instead of hostname** (no SPN = no Kerberos)
- Non-domain joined machines
- Legacy apps

**Tip:** Force NTLM by using IP addresses instead of hostnames


**Key Attacks**
| Attack | Tool |
|---|---|
| Capture hash (relay/poison) | Responder |
| Relay captured hash | ntlmrelayx.py |
| Pass-the-Hash | crackmapexec, psexec.py |
| Crack captured hash | hashcat (`-m 5600` for NTLMv2) |


**Impacket Auth**
```bash
smbclient.py domain/user:'password'@<IP>
```
- Uses NTLM under the hood when no Kerberos available
- Core toolkit: `psexec.py`, `wmiexec.py`, `secretsdump.py`

**NTLM Authentication Flow**

1. Authentication Request
   Client → Server
   Send username

2. Challenge
   Server → Client
   Send random challenge (nonce)

3. Response
   Client → Server
   Encrypt challenge using NT Hash
   Send response

4. Verification Request
   Server → Domain Controller
   Send:

   * Username
   * Challenge
   * Response

5. Verification
   Domain Controller
   Recalculates response using stored NT Hash

6. Authentication Result
   Domain Controller → Server
   Valid / Invalid

7. Access Granted
   Server → Client
   Allow or deny access

**Critical Weakness to Remember**
No mutual authentication → client can't verify server identity → **NTLM relay** works by sitting in the middle and forwarding auth to a different target service

<br>

**Key Components**
- **KDC** — runs on DC, contains AS + TGS
- **KRBTGT** — special account; its hash encrypts ALL TGTs → compromise = Golden Ticket
- **TGT** — primary ticket, get more tickets with this
- **ST (Service Ticket)** — access specific service, encrypted with service account hash
- **SPN** — ties a service to an account (why hostname required, not IP)


**Attack Surface**
| Attack | What you need | What you get |
|---|---|---|
| **Kerberoasting** | Any valid domain user | ST encrypted with service hash → crack offline |
| **AS-REP Roasting** | Account with pre-auth disabled | Encrypted AS-REP → crack offline |
| **Pass-the-Ticket** | ccache file or `.kirbi` | Authenticate as user, no password needed |
| **Golden Ticket** | KRBTGT hash | Forge any TGT → permanent domain access |
| **Silver Ticket** | Service account hash | Forge ST → access specific service |


**ccache Files (Linux)**
```bash
# Default location
/tmp/krb5cc_<uid>

# View tickets
klist

# Use a stolen ticket
export KRB5CCNAME=stolen.ccache
```

**Impacket Kerberos Workflow**
```bash
# 1. Get TGT
getTGT.py domain/user:'pass' -dc-ip <DC_IP>

# 2. Export ticket
export KRB5CCNAME=user.ccache

# 3. Use ticket (hostname not IP)
smbclient.py domain/user@HOSTNAME -k -no-pass
```

**Remember:** Kerberos needs hostname → always add to `/etc/hosts` when attacking


Kerberos Authentication Flow

1. AS-REQ
   Client → KDC
   Send username + encrypted timestamp

2. AS-REP
   KDC → Client
   Return:

   * Session Key
   * TGT (Ticket Granting Ticket)

3. TGS-REQ
   Client → KDC
   Send:

   * TGT
   * SPN (requested service)
   * Authenticator (encrypted with Session Key)

4. TGS-REP
   KDC → Client
   Return:

   * Service Ticket (ST)
   * Service Session Key

5. AP-REQ
   Client → Service
   Present Service Ticket (ST)

6. Service validates ST
   Service decrypts ticket using its own hash

7. Authentication successful

<br>



**NTLM Weaknesses**
- **Unsalted MD4** → rainbow tables + fast GPU cracking
- **Hash = password** → Pass-the-Hash, no need to crack
- **No mutual auth** → NTLM Relay, MitM
- **Downgrade possible** → force systems off Kerberos onto NTLM


**Kerberos Weaknesses**
- **Any user can request TGS** → Kerberoasting (crack offline)
- **Pre-auth optional** → AS-REP Roasting (no creds needed)
- **Tickets stored in memory** → Pass-the-Ticket
- **Hash → ticket conversion** → Overpass-the-Hash
- **KRBTGT hash exposed** → Golden Ticket (forge any TGT)
- **Service account hash exposed** → Silver Ticket (forge specific TGS)


**Config-Based (both protocols)**
- Weak passwords → cracking/spraying
- Misconfigured delegation → privesc
- Stale accounts → easy targets
- Password spraying → bypasses lockout if done slowly


**1. Hash Cracking**
```bash
hashcat -m 1000 hash.txt rockyou.txt      # crack NTLM
hashcat -m 1000 hash.txt --show           # view result
```
Format: `939B0058BC6DD834ABC4CC08CFEFEA69`


**2. Pass-the-Hash**
```bash
smbclient.py domain/user@<IP> -hashes aad3b435b51404eeaad3b435b51404ee:<NTLM_HASH>
```
- LM portion is always `aad3b435b51404eeaad3b435b51404ee` (empty/dummy)


**3. Kerberoasting**
```bash
GetUserSPNs.py domain/user:'pass' -dc-ip <DC> -request   # dump TGS hashes
hashcat -m 13100 ticket.txt rockyou.txt                   # crack TGS
```
Hash starts with `$krb5tgs$23$`


**4. Golden Ticket**
```bash
# Need: KRBTGT hash + Domain SID
ticketer.py -nthash <KRBTGT_HASH> -domain-sid <SID> -domain <domain> Administrator
export KRB5CCNAME=Administrator.ccache
smbclient.py domain/Administrator@HOSTNAME -k -no-pass
```

<br>


**Key Event IDs**
| ID | What it detects |
|---|---|
| 4624 | Successful logon → check Auth Package + Logon Type |
| 4625 | Failed logon → password spraying |
| 4768 | TGT requested |
| 4769 | TGS requested → Kerberoasting |
| 4771 | Kerberos pre-auth failed → AS-REP roasting / brute force |


**Detection Indicators**

**Pass-the-Hash:**
- 4624 with `Auth Package: NTLM` + `Logon Type: 3` + blank source IP

**Kerberoasting:**
- Spike of 4769 from single account
- Encryption type `0x17` (RC4) instead of `0x12` (AES-256) → deliberate downgrade

**AS-REP Roasting:**
- Spike of 4771 across many accounts


**Mitigations (know for bypassing/OPSEC)**
| Attack | Defense to expect |
|---|---|
| PtH | Protected Users group, NTLM disabled |
| NTLM Relay | SMB signing enforced, EPA enabled |
| Kerberoasting | gMSA accounts, strong svc passwords |
| Golden Ticket | KRBTGT reset twice |
| Spray | Lockout policy, 4625 monitoring |

<br>
<br>


