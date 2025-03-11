# IDOR



### What is IDOR

**Main Topic:** IDOR (Insecure Direct Object Reference) is a flaw letting users grab stuff they shouldn’t.  
- **What It Is:** Web server trusts user input too much—like an ID number—to fetch files or data, without checking if it’s theirs.

**Example:** You’re on a site, change `user=123` to `user=124` in the URL, and see someone else’s profile—oops, no server check!

**Remembering Tip:** Think of IDOR as a “library card trick”—swap the number, grab any book if they don’t verify!

---



### Finding IDORs with Encoded IDs

**Main Topic:** Spot IDORs by messing with Base64-encoded IDs.  
- **What’s Happening:** Web devs encode data (like user IDs) into Base64 (A-Z, a-z, 0-9, =) for pages, but don’t always check if you own it.  

**How to Test:**  
- Grab a Base64 string (e.g., from a URL like `id=TWFu`).  
- Decode it at `base64decode.org`—say it’s “Man” (user ID?).  
- Tweak it to “Bob,” re-encode at `base64encode.org` (gets `Qm9i`), resubmit—see if Bob’s stuff shows up!

**Example:** URL `site.com/profile?id=TWFu` shows your profile. Change it to `id=Qm9i`—oops, Bob’s profile pops up!

**Remembering Tip:** Think of Base64 as a “secret note”—crack it, rewrite it, and sneak into someone else’s locker!

---


### Finding IDORs with Hashed IDs

**Main Topic:** Crack IDORs by guessing hashed IDs that follow a pattern.  
- **What’s Up:** IDs get hashed (e.g., MD5 turns 123 into `202cb962ac59075b964b07152d234b70`), but if they’re predictable (like numbers), you can still mess with them.

**How to Test:**  
- See an ID like `202cb962ac59075b964b07152d234b70` in a URL.  
- Guess it’s hashed numbers—try MD5 of 124 (`250cf8b51c773f3f8dc8b4be867a9a02`), swap it in, check if it pulls someone else’s data.

**Example:** `site.com/user?id=202cb962ac59075b964b07152d234b70` (123) shows your profile. Change to `250cf8b51c773f3f8dc8b4be867a9a02` (124)—bam, someone else’s!

**Remembering Tip:** Think of hashed IDs as a “number lock”—guess the next combo to sneak in!

---


### Finding IDORs with Unpredictable IDs

**Main Topic:** Spot IDORs by swapping random IDs between accounts.  
- **What’s Up:** If IDs are wild (not guessable), test by flipping them between two users.

**How to Test:**  
- Make two accounts—say, yours (ID: `xyz123`) and a dummy (ID: `abc789`).  
- Log in as you, swap to `abc789` in the URL—if you see the dummy’s stuff, it’s an IDOR!

**Example:** `site.com/profile?id=xyz123` is yours. Change to `id=abc789`—whoa, dummy’s profile shows up!

**Remembering Tip:** Think of it as “swapping backstage passes”—sneak into someone else’s VIP area!

---


### Where IDORs Hide

**Main Topic:** IDORs can lurk beyond the URL bar—check sneaky spots.  
- **Where to Look:** AJAX calls, JavaScript files, or hidden parameters, not just the address bar.

**Example:**  
- Site loads `/user/details` for your info. Dig in JS, find `user_id`.  
- Try `/user/details?user_id=123`—bam, someone else’s details pop up!

**Remembering Tip:** Think of IDORs as “hidden keys”—hunt in the site’s back pockets, not just the front door!

