# Content Discovery


### Content Discovery Basics

**Main Idea:** Find hidden stuff on websites that’s not out in the open.

**What’s Content?**  
- Files, pics, backups, staff pages—stuff not meant for everyone.

**Examples:**  
- Secret admin panels, old site versions, config files.

**3 Ways to Find It:**  
- **Manual:** Poke around yourself (e.g., check `/admin`).  
- **Automated:** Use tools to scan fast.  
- **OSINT:** Dig public info (e.g., old links online).

**Why It’s Cool:** Uncovers juicy bits site owners might not want you to see.

**Remembering Tip:** Think of it as “website hide-and-seek”—hunt for the sneaky stuff!

---


### Robots.txt Discovery

**Main Idea:** Check `robots.txt` to find hidden website spots pen testers can explore.

**What’s Robots.txt?**  
- A file telling search engines what to skip (e.g., admin pages, customer files).  
- Lives at `http://MACHINE_IP/robots.txt` (updates 2 mins after machine starts).

**Example (Acme IT Support):**  
- Open Firefox on AttackBox, go to `http://MACHINE_IP/robots.txt`.  
- Look for blocked paths—like `/admin` or `/private`—they’re clues to secret areas!

**Why It’s Cool:** Owners hide stuff here, but it’s a treasure map for us testers.

**Remembering Tip:** Think of `robots.txt` as a “do not enter” sign—perfect place to sneak a peek!

---


### Favicon Discovery

**Main Idea:** A website’s favicon (tab icon) can spill secrets about its framework.

**What’s a Favicon?**  
- Tiny logo in your browser tab, like a site’s brand badge.

**Why It Helps:**  
- Lazy devs leave default favicons from frameworks—clues to the tech stack.  
- Check hashes against OWASP’s favicon database (`https://wiki.owasp.org/index.php/OWASP_favicon_database`).

**Example (AttackBox):**  
- Open Firefox, go to `https://static-labs.tryhackme.cloud/sites/favicon/`.  
- See `images/favicon.ico` in page source.  
- Grab it:  
  - Linux: `curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum`  
  - Windows: `curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico -o favicon.ico; Get-FileHash .\favicon.ico -Algorithm MD5`  
- Match hash to OWASP list—find the framework!

**Tip:** If curl fails (hash ends in 427e), retry or use a VM.

**Remembering Tip:** Think of favicon as a “site’s fingerprint”—match it to catch the framework culprit!

---


### Sitemap.xml Discovery

**Main Idea:** `sitemap.xml` shows pages a website wants search engines to find—sometimes sneaky ones too.

**What’s Sitemap.xml?**  
- A list of URLs the site owner wants indexed (unlike `robots.txt` that hides stuff).  
- Might reveal hard-to-find or old pages still active.

**Example:**  
- Check `http://MACHINE_IP/sitemap.xml`—could list `/old-page` or `/secret-area` not linked anywhere.

**Why It’s Cool:** Dig up hidden or forgotten corners of a site.

**Remembering Tip:** Think of `sitemap.xml` as a “website’s brag list”—shows off pages, even ones they forgot to hide!

---


### HTTP Headers Discovery

**Main Idea:** HTTP headers from a web server can spill tech details for pen testing.

**What’s HTTP Headers?**  
- Info sent back with every web request (e.g., server type, language).  

**Example:**  
- Run: `curl -v http://MACHINE_IP`  
- See: `Server: nginx/1.18.0` and `X-Powered-By: PHP/7.4.3`—check if those versions have bugs!

**Why It’s Cool:** Reveals software and versions to hunt for known weaknesses.

**Remembering Tip:** Think of headers as a “server’s name tag”—tells you who’s running the show!

---


### Framework Stack Discovery

**Main Idea:** Spot a website’s framework to uncover more goodies.

**How to Find It:**  
- Check page source for clues (comments, credits) or favicon hints.  

**Example (Acme IT Support):**  
- At `http://MACHINE_IP`, see a comment with load time and a link: `https://static-labs.tryhackme.cloud/sites/thm-web-framework`.  
- Visit that site, check docs—finds the admin portal path.  
- Try it on Acme (e.g., `/admin`)—grabs a flag!

**Why It’s Cool:** Framework details lead to secret spots like admin pages.

**Remembering Tip:** Think of framework as a “website’s recipe”—find it, and you’ll sniff out the hidden ingredients!

---


### Google Hacking/Dorking

**Main Idea:** Use Google tricks to find hidden stuff on a target website.

**What’s Dorking?**  
- OSINT (free info) with Google’s search filters to dig up content.

**Key Filters:**  
- `site:` - Limit to one site (e.g., `site:tryhackme.com`).  
- `inurl:` - Word in URL (e.g., `inurl:admin`).  
- `filetype:` - File type (e.g., `filetype:pdf`).  
- `intitle:` - Word in title (e.g., `intitle:admin`).

**Example:**  
- Search `site:tryhackme.com inurl:admin`—finds admin pages on TryHackMe.

**Why It’s Cool:** Uncovers secret pages or files Google’s already sniffed out.

**Remembering Tip:** Think of dorking as “Google’s treasure hunt”—filter the map to find the loot!

---


### Wappalyzer OSINT

**Main Idea:** Wappalyzer sniffs out a website’s tech stack for free intel.

**What It Does:**  
- Online tool and browser extension (`https://www.wappalyzer.com/`).  
- Spots frameworks, CMS (e.g., WordPress), payment systems, even version numbers.

**Example:**  
- Visit a site, click the Wappalyzer icon—see it’s using Drupal 9.5 or Stripe.

**Why It’s Cool:** Quick way to map a site’s guts for pen testing or competitor spying.

**Remembering Tip:** Think of Wappalyzer as a “website X-ray”—sees through to the tech bones!

---


### Wayback Machine OSINT

**Main Idea:** Wayback Machine digs up a website’s past for hidden clues.

**What It Is:**  
- A web archive since the ‘90s (`https://archive.org/web/`).  
- Search a domain, see old snapshots of its pages.

**Example:**  
- Check `tryhackme.com`—find an old `/login` page still lurking.

**Why It’s Cool:** Spots forgotten pages or features still live on the site.

**Remembering Tip:** Think of Wayback as a “website time capsule”—unearths old secrets!

---


Here’s a short, simple note for your GitHub based on the "OSINT - GitHub" script. I’ve kept it easy with a quick example and a tip!

---


### GitHub OSINT

**Main Idea:** GitHub’s public repos can leak target info like code or secrets.

**What’s GitHub?**  
- Built on Git (tracks file changes for teams).  
- Hosts repos online—public or private.  

**How It Helps:**  
- Search company/site names (e.g., “acme it support”).  
- Find source code, passwords, or hidden stuff.

**Example:**  
- Search “acme” on GitHub, spot a public repo with old login code.

**Why It’s Cool:** Free peek at what devs forgot to lock up.

**Remembering Tip:** Think of GitHub as a “dev’s messy desk”—rifle through for juicy scraps!

---


### S3 Buckets OSINT

**Main Idea:** S3 Buckets (AWS storage) can leak files if permissions are sloppy.

**What’s S3?**  
- Cloud storage by Amazon (e.g., `https://tryhackme-assets.s3.amazonaws.com`).  
- Owners set access—public, private, or writable.

**How to Find ‘Em:**  
- Spot URLs in page source or GitHub.  
- Guess with names like `{company}-assets`, `{company}-public`.  

**Example:**  
- Try `acme-public.s3.amazonaws.com`—might dump private files if misconfigured.

**Why It’s Cool:** Bad settings = free access to stuff they didn’t mean to share.

**Remembering Tip:** Think of S3 as a “cloud closet”—peek in if the door’s unlocked!

---


### Automated Discovery

**Main Idea:** Use tools to auto-find hidden website stuff fast.

**What’s Automated Discovery?**  
- Tools blast tons of requests to a web server to spot files or directories.  

**Wordlists:**  
- Text files with common names (e.g., `admin`, `login`).  
- Check `SecLists` on AttackBox (`https://github.com/danielmiessler/SecLists`).

**Top Tools (On AttackBox):**  
- **ffuf:** Fast, flexible scanner.  
- **dirb:** Simple directory buster.  
- **gobuster:** Quick and reliable.  

**Example:**  
- Run `ffuf -w wordlist.txt -u http://MACHINE_IP/FUZZ`—finds `/secret` if it’s there.

**Why It’s Cool:** Beats manual clicking—digs up content in seconds.

**Remembering Tip:** Think of it as a “website vacuum”—sucks up hidden bits with wordlists!



