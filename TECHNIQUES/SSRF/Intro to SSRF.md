# Intro to SSRF


### SSRF Basics

**Main Topic:** SSRF (Server-Side Request Forgery) tricks a server into fetching stuff for an attacker.  
- **What It Is:** Bad guy makes the server send HTTP requests to places they pick.  
- **Types:** Regular (you see the data), Blind (no data shows up).

**Example:** Site lets you upload a pic from a URL. You sneak in `http://secret.server`—server grabs it for you!

**Remembering Tip:** Think of SSRF as a “server puppet”—pull its strings to fetch your sneaky stuff!

---


