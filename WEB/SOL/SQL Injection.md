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


