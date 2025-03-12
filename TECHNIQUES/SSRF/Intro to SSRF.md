# Intro to SSRF


### SSRF Basics

**Main Topic:** SSRF (Server-Side Request Forgery) tricks a server into fetching stuff for an attacker.  
- **What It Is:** Bad guy makes the server send HTTP requests to places they pick.  
- **Types:** Regular (you see the data), Blind (no data shows up).

**Example:** Site lets you upload a pic from a URL. You sneak in `http://secret.server`—server grabs it for you!

**Remembering Tip:** Think of SSRF as a “server puppet”—pull its strings to fetch your sneaky stuff!

---


### What’s `&x=` in SSRF? 

**Main Topic:** `&x=` is a trick to stop extra URL junk from messing up an SSRF attack.  
- **Why It’s There:** When you tweak a URL, leftover bits (like `id=2`) might stick to your attack path. `&x=` turns them into a harmless query parameter.

**Easy Example:**  
- Normal URL: `website.thm/stock/item?id=2`—server grabs `/stock/item`.  
- You tweak to: `website.thm/stock/../api/user`—aims for `/api/user`, but `?id=2` might glue onto `/api/user?id=2`, making a mess.  
- Add `&x=`: `website.thm/stock/../api/user&x=`—now it’s `/api/user?x=` and `id=2` gets ignored or separated, keeping your attack clean!

**Remembering Tip:** Think of `&x=` as a “URL janitor”—sweeps extra baggage into a side bin so your sneaky path stays clear!

---


### Spotting SSRF Holes

**Main Topic:** Find SSRF weak spots where a web app grabs URLs you can tweak.  
- **Where to Look:**  
  1. Full URL in address bar: `site.com?page=http://evil.com`  
  2. Hidden form field: `<input type="hidden" value="server.com">`  
  3. Just a hostname: `site.com?host=internal.server`  
  4. URL path only: `site.com?path=/secret`  

**Example:** `site.com?host=server.com`—change to `evil.com` and see if it fetches your stuff!

**Tip for Blind SSRF:** No output? Use `requestbin.com` or Burp Collaborator to catch what the server pings.

**Remembering Tip:** Think of SSRF spots as “server fetch buttons”—push the wrong one, and it’s your party!

---


### Beating SSRF Defenses

**Main Topic:** Sneak past SSRF blocks like deny lists, allow lists, or use open redirects.  

**How It Works:**  
- **Deny List:** Blocks stuff like `localhost` (127.0.0.1). Try `127.1` or `0.0.0.0`—slips through!  
- **Allow List:** Only lets `https://website.thm`. Use `website.thm.evil.com`—it’s allowed but yours!  
- **Open Redirect:** Site has `website.thm/link?url=tryhackme.com`. Feed it `website.thm/link?url=evil.com`—server hops to your spot.

**Example:** App blocks `169.254.169.254` (cloud data). Point `cloud.evil.com` to it—server fetches your fake anyway!

**Remembering Tip:** Think of SSRF defenses as “picky bouncers”—swap IDs (`127.1`), fake a VIP pass (`website.thm.evil`), or sneak through a side door (redirect)!
