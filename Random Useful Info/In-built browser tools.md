# in-built browser tools



### Exploring Websites

**Main Idea:** As a pen tester, scout a website for interactive spots that might be weak.

**How to Start:**  
- Use your browser to poke around.  
- Look for stuff users can mess with (e.g., login forms, buttons).  
- List pages, URLs, and what they do.

**Example: Acme IT Support Site:**  
- **Home:** `/` - Company intro, staff pic.  
- **News:** `/news` - Article list (e.g., `/news/article?id=1`).  
- **Contact:** `/contact` - Form (name, email, message).  
- **Login:** `/customers/login` - Username/password fields.  
- **Signup:** `/customers/signup` - New user form.  
- **Ticket:** `/customers/ticket/new` - Issue box + file upload.

**Why It Matters:** Interactive bits (forms, uploads) are where bugs hide—find ‘em to test ‘em!

**Remembering Tip:** Think of it as “website treasure hunting”—map the spots where users play, that’s where trouble might lurk!

---


### Viewing Page Source

**Main Idea:** Check a website’s code (HTML, CSS, JavaScript) to find hidden clues.

**How to Do It:**  
- Right-click > “View Page Source.”  
- Or type `view-source:` before the URL (e.g., `view-source:https://acme.com`).  
- Or use browser menu (e.g., Developer Tools).

**What to Look For (Acme IT Support Example):**  
- **Comments:** `<!-- stuff -->`—dev notes (e.g., temp homepage link with a flag).  
- **Links:** `<a href="...">`—hidden pages (e.g., “secr” link for a flag).  
- **External Files:** CSS/JS dirs (e.g., directory listing shows `flag.txt`).  
- **Framework Clues:** Bottom comment—outdated framework version (check update notice for a flag).

**Why It’s Cool:** Spots secrets like private pages or old code with known bugs.

**Remembering Tip:** Think of page source as a “website’s diary”—sneaky comments and links spill the beans!

---


### Inspector in Developer Tools

**Main Idea:** Use the Inspector in browser dev tools to see and tweak what’s live on a webpage.

**How to Open:**  
- Right-click > “Inspect” (or check browser menu for dev tools).  

**What It Does:**  
- Shows real-time HTML/CSS (unlike static page source).  
- Lets you edit stuff on the fly—like a sandbox.

**Example (Acme IT News):**  
- Go to `/news`, see a “premium only” block on article 3.  
- Right-click the block > Inspect.  
- Find `<div class="premium-customer-blocker">`, spot `display: block` in CSS.  
- Change `block` to `none`—block vanishes, flag appears!

**Why It’s Cool:** Reveals hidden content or tests fixes (only in your browser—refresh resets it).

**Remembering Tip:** Think of Inspector as a “website remote”—tune the live show to find secrets!

---


### Debugger in Developer Tools

**Main Idea:** Use the Debugger to peek into and pause JavaScript on a webpage.

**How to Use:**  
- Open dev tools (e.g., “Debugger” in Firefox, “Sources” in Chrome).  
- Find JS files on the left (e.g., `flash.min.js` in `/assets`).

**Example (Acme IT Contact Page):**  
- Notice a red flash? Go to `/contact`, open Debugger.  
- Pick `flash.min.js`—it’s minified (squished) and obfuscated (messy).  
- Click `{}` (Pretty Print) to tidy it a bit.  
- Scroll to `flash['remove']();`—this hides the red box.  
- Click the line number to set a blue breakpoint, refresh—red box stays, flag pops up!

**Why It’s Cool:** Stops JS in its tracks to reveal hidden stuff (like that red flag).

**Remembering Tip:** Think of Debugger as a “JS time-freezer”—pause the action to catch sneaky secrets!

---



### Network in Developer Tools

**Main Idea:** Use the Network tab to watch a webpage’s outside calls.

**How to Use:**  
- Open dev tools, click “Network,” refresh the page.  
- See every file request (clear with trash can if messy).

**Example (Acme IT Contact Page):**  
- Go to `/contact`, open Network tab, refresh.  
- Fill the contact form, hit “Send Message.”  
- Spot a new entry—form data sent via AJAX (background trick).  
- Check that entry’s page link—finds a flag!

**Why It’s Cool:** Catches sneaky data sends (like form submits) you’d miss otherwise.

**Remembering Tip:** Think of Network tab as a “website phone log”—tracks every call it makes!
