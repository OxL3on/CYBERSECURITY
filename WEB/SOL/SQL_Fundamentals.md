## **Databases 101**


#### **1. What is a Database?**
- **Definition**: A database is like a digital filing cabinet that stores organized information (data) so it can be easily accessed, managed, or analyzed.
- **Example**: 
  - Netflix uses a database to store your watch history and recommend shows.
  - Instagram stores posts, likes, and comments in a database.

**Remember**: Think of a database as a "smart storage box" for all kinds of data.


#### **2. Types of Databases**
There are two main types of databases:

1. **Relational Databases (SQL)**:
   - Data is stored in tables with rows and columns (like an Excel sheet).
   - Example: An e-commerce site storing user info (name, email, password) in a structured way.
   - Best for: Data that has a consistent format (e.g., transactions).

2. **Non-Relational Databases (NoSQL)**:
   - Data is stored in flexible formats like key-value pairs, documents, or collections.
   - Example: Storing scanned documents where each document has different fields.
   - Best for: Data that varies in format (e.g., social media posts).

**Remember**: Relational = Structured (like a table), Non-relational = Flexible (like a folder).


#### **3. Tables, Rows, and Columns**
- **Table**: A collection of related data (e.g., a "Books" table for book info).
- **Columns**: Define the type of data (e.g., "ID", "Name", "Published Date").
- **Rows**: Each row is a record (e.g., one book's details).

**Example**:  
| ID | Name                     | Published Date |
|----|--------------------------|----------------|
| 1  | Android Security Internals | 2014-10-14     |

**Remember**: Table = Grid, Columns = Categories, Rows = Entries.


#### **4. Primary and Foreign Keys**
- **Primary Key**: A unique identifier for each record in a table (e.g., "ID" in the Books table).
  - Example: Matriculation numbers in a university—each student has a unique number.
- **Foreign Key**: Links two tables together by referencing the primary key of another table.
  - Example: Adding an "author_id" column in the "Books" table links it to the "Authors" table.

**Remember**:  
- Primary Key = Unique ID for a table.  
- Foreign Key = Bridge between two tables.


### **-----**
Imagine you own a bookstore:
- You create a **table** called "Books" with **columns** like "ID", "Name", and "Published Date".
- Each book is a **row** in the table.
- To track authors, you create another table called "Authors" and link it to the "Books" table using a **foreign key** (e.g., "author_id").
- Every book gets a **primary key** (its unique ID), and every author also gets a unique ID.

Now, when someone asks for a book, you can quickly find both the book and its author!


### **Key Takeaways**
1. Databases store and organize data for easy access.
2. Relational databases use tables, while non-relational databases are more flexible.
3. Tables have rows (records) and columns (categories).
4. Primary keys uniquely identify records; foreign keys connect tables.

**Tip**: Think of databases as a library—books (data) are organized on shelves (tables), and labels (keys) help you find what you need!


---
---


## **SQL**


#### **1. What is SQL?**
- **Definition**: SQL (Structured Query Language) is a programming language used to interact with relational databases.
- **Purpose**: It helps you create, read, update, and delete data in a database.
- **Example**: 
  - Imagine a library database. You can use SQL to:
    - Add new books (`INSERT`).
    - Search for books by title (`SELECT`).
    - Update book details (`UPDATE`).
    - Remove books (`DELETE`).

**Remember**: SQL = The "language" you use to talk to databases.


#### **2. Database Management System (DBMS)**
- A DBMS is software that acts as a bridge between you (the user) and the database.
- **Examples of DBMS**:
  - MySQL
  - MongoDB
  - Oracle Database
  - MariaDB

**Remember**: Think of DBMS as a "control panel" for managing databases.


#### **3. Benefits of SQL**
1. **Fast**: Relational databases process data quickly because they are optimized for speed and storage.
2. **Easy to Learn**: SQL uses simple English-like commands (e.g., `SELECT`, `INSERT`, `UPDATE`).
3. **Reliable**: Data follows strict rules, ensuring accuracy.
4. **Flexible**: You can perform complex queries to analyze or manipulate data.


#### **4. Getting Hands-On with SQL**
To start using SQL, follow these steps:

1. **Start MySQL**:
   - Open the terminal and type:
     ```bash
     mysql -u root -p
     ```
   - Enter the password when prompted:
     ```
     tryhackme
     ```

2. **Welcome Screen**:
   - After logging in, you’ll see something like this:
     ```
     Welcome to the MySQL monitor. Commands end with ; or \g.
     ```

3. **Start Using SQL**:
   - You’re now ready to write SQL commands! For example:
     ```sql
     SHOW DATABASES;
     ```
     This command lists all available databases.

**Remember**: Always end SQL commands with a semicolon (`;`).


### **-----**
Imagine you’re a librarian managing a digital library:
- You use **MySQL** (a DBMS) to access your library database.
- You write **SQL commands** to:
  - Add new books (`INSERT INTO Books`).
  - Find books by author (`SELECT * FROM Books WHERE Author = 'J.K. Rowling'`).
  - Update book details (`UPDATE Books SET Title = 'New Title' WHERE ID = 1`).
  - Delete books (`DELETE FROM Books WHERE ID = 2`).

With SQL, you can manage your library efficiently and find what you need in seconds!

### **Key Takeaways**
1. SQL is the language used to interact with relational databases.
2. DBMS (like MySQL) is the tool that connects you to the database.
3. SQL is fast, easy to learn, reliable, and flexible.
4. To get started, log into MySQL using `mysql -u root -p` and explore databases with commands like `SHOW DATABASES;`.


---
---


### **Database and Table Statements in SQL**


#### **1. Database Statements**

1. **CREATE DATABASE**  
   - Creates a new database.
   - Syntax:  
     ```sql
     CREATE DATABASE database_name;
     ```
   - Example:  
     ```sql
     CREATE DATABASE thm_bookmarket_db;
     ```

2. **SHOW DATABASES**  
   - Lists all available databases.
   - Syntax:  
     ```sql
     SHOW DATABASES;
     ```

3. **USE DATABASE**  
   - Selects a database to work with.
   - Syntax:  
     ```sql
     USE database_name;
     ```
   - Example:  
     ```sql
     USE thm_bookmarket_db;
     ```

4. **DROP DATABASE**  
   - Deletes a database permanently.
   - Syntax:  
     ```sql
     DROP DATABASE database_name;
     ```
   - **Caution**: Be careful! Once deleted, the database cannot be recovered.

**Remember**: Think of databases as folders. You create, open, or delete them depending on your needs.


#### **2. Table Statements**
Once you’ve selected a database, you can create and manage tables within it.

1. **CREATE TABLE**  
   - Creates a table with columns and data types.
   - Syntax:  
     ```sql
     CREATE TABLE table_name (
         column1 data_type,
         column2 data_type,
         ...
     );
     ```
   - Example:  
     ```sql
     CREATE TABLE book_inventory (
         book_id INT AUTO_INCREMENT PRIMARY KEY,
         book_name VARCHAR(255) NOT NULL,
         publication_date DATE
     );
     ```
     - `book_id`: A unique ID for each book (auto-increments).
     - `book_name`: The name of the book (cannot be empty).
     - `publication_date`: The date the book was published.

2. **SHOW TABLES**  
   - Lists all tables in the active database.
   - Syntax:  
     ```sql
     SHOW TABLES;
     ```

3. **DESCRIBE**  
   - Shows details about a table’s structure (columns, data types, etc.).
   - Syntax:  
     ```sql
     DESCRIBE table_name;
     ```
   - Example:  
     ```sql
     DESCRIBE book_inventory;
     ```

4. **ALTER TABLE**  
   - Modifies an existing table (e.g., adding or changing columns).
   - Syntax:  
     ```sql
     ALTER TABLE table_name ADD column_name data_type;
     ```
   - Example:  
     ```sql
     ALTER TABLE book_inventory ADD page_count INT;
     ```

5. **DROP TABLE**  
   - Deletes a table permanently.
   - Syntax:  
     ```sql
     DROP TABLE table_name;
     ```
   - **Caution**: Once dropped, the table and its data are gone forever.

**Remember**: Tables are like spreadsheets. You define their structure (columns), fill them with data (rows), and can modify or delete them as needed.


### **Quick Recap Story**
Imagine you’re setting up a digital bookstore:
1. **Create a Database**:  
   - You create a database called `thm_bookmarket_db` to store all your bookstore data.
   - Command:  
     ```sql
     CREATE DATABASE thm_bookmarket_db;
     ```

2. **Select the Database**:  
   - You tell MySQL to use this database for your work.
   - Command:  
     ```sql
     USE thm_bookmarket_db;
     ```

3. **Create a Table**:  
   - You create a table called `book_inventory` to store book details like ID, name, and publication date.
   - Command:  
     ```sql
     CREATE TABLE book_inventory (
         book_id INT AUTO_INCREMENT PRIMARY KEY,
         book_name VARCHAR(255) NOT NULL,
         publication_date DATE
     );
     ```

4. **View Tables**:  
   - You check if the table was created successfully.
   - Command:  
     ```sql
     SHOW TABLES;
     ```

5. **Modify the Table**:  
   - Later, you decide to add a `page_count` column to track how many pages each book has.
   - Command:  
     ```sql
     ALTER TABLE book_inventory ADD page_count INT;
     ```

6. **Describe the Table**:  
   - You inspect the table structure to confirm the changes.
   - Command:  
     ```sql
     DESCRIBE book_inventory;
     ```


### **Key Takeaways**
1. **Database Commands**:
   - Create (`CREATE DATABASE`), View (`SHOW DATABASES`), Use (`USE DATABASE`), Delete (`DROP DATABASE`).

2. **Table Commands**:
   - Create (`CREATE TABLE`), View (`SHOW TABLES`), Inspect (`DESCRIBE`), Modify (`ALTER TABLE`), Delete (`DROP TABLE`).

3. **Best Practices**:
   - Always double-check before using `DROP` commands.
   - Define primary keys to uniquely identify records.
   - Use `NOT NULL` for columns that must always have a value.

**Tip**: Think of databases as filing cabinets and tables as folders inside them. Organize carefully, and you’ll always find what you need!


---
---


### **CRUD Operations**

#### **1. What is CRUD?**
CRUD stands for **Create, Read, Update, and Delete**—the four basic operations used to manage data in a database.


#### **2. CRUD Operations Explained**

1. **Create (INSERT)**  
   - Adds new records to a table.
   - Syntax:  
     ```sql
     INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
     ```
   - Example:  
     ```sql
     INSERT INTO books (id, name, published_date, description)
     VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
     ```
   - **Tip**: Always specify the columns you’re inserting into to avoid errors.

2. **Read (SELECT)**  
   - Retrieves data from a table.
   - Syntax:  
     ```sql
     SELECT column1, column2, ... FROM table_name;
     ```
   - To retrieve all columns:  
     ```sql
     SELECT * FROM table_name;
     ```
   - Example:  
     ```sql
     SELECT name, description FROM books;
     ```
   - **Tip**: Use `WHERE` to filter specific rows. Example:  
     ```sql
     SELECT * FROM books WHERE id = 1;
     ```

3. **Update (UPDATE)**  
   - Modifies existing records in a table.
   - Syntax:  
     ```sql
     UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
     ```
   - Example:  
     ```sql
     UPDATE books
     SET description = "An In-Depth Guide to Android's Security Architecture."
     WHERE id = 1;
     ```
   - **Caution**: Always include a `WHERE` clause to avoid updating all rows accidentally.

4. **Delete (DELETE)**  
   - Removes records from a table.
   - Syntax:  
     ```sql
     DELETE FROM table_name WHERE condition;
     ```
   - Example:  
     ```sql
     DELETE FROM books WHERE id = 1;
     ```
   - **Caution**: Be careful with `DELETE`. Without a `WHERE` clause, it will delete all rows in the table.


### **-----**
Imagine you’re managing a library’s digital bookshelf:
1. **Create**: You add a new book to the system:
   ```sql
   INSERT INTO books (id, name, published_date, description)
   VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide...");
   ```

2. **Read**: You check the details of all books:
   ```sql
   SELECT * FROM books;
   ```

3. **Update**: You fix a typo in the book’s description:
   ```sql
   UPDATE books
   SET description = "An In-Depth Guide to Android's Security Architecture."
   WHERE id = 1;
   ```

4. **Delete**: You remove a book that’s no longer available:
   ```sql
   DELETE FROM books WHERE id = 1;
   ```


### **Key Takeaways**
1. **CRUD Operations**:
   - **Create**: Add new data (`INSERT`).
   - **Read**: Retrieve data (`SELECT`).
   - **Update**: Modify data (`UPDATE`).
   - **Delete**: Remove data (`DELETE`).

2. **Best Practices**:
   - Always use a `WHERE` clause with `UPDATE` and `DELETE` to avoid unintended changes.
   - Use `SELECT` to verify data before making changes.
   - Specify columns explicitly in `INSERT` for clarity.

**Tip**: Think of CRUD as the four actions you’d take with a filing cabinet: Add files, look at files, update files, and remove files.

---
---


### **SQL Clauses**


#### **1. What are Clauses?**
Clauses are parts of SQL statements that refine how data is retrieved, sorted, or grouped. They help you control the results of your queries.


#### **2. Key Clauses Explained**

1. **DISTINCT Clause**  
   - Removes duplicate rows and returns only unique values.
   - Syntax:  
     ```sql
     SELECT DISTINCT column_name FROM table_name;
     ```
   - Example:  
     ```sql
     SELECT DISTINCT name FROM books;
     ```
   - **Tip**: Use `DISTINCT` when you want to avoid seeing repeated data in your results.

2. **GROUP BY Clause**  
   - Groups rows with similar values into summary rows (e.g., counts, sums).
   - Often used with aggregate functions like `COUNT`, `SUM`, or `AVG`.
   - Syntax:  
     ```sql
     SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
     ```
   - Example:  
     ```sql
     SELECT name, COUNT(*) FROM books GROUP BY name;
     ```
   - **Tip**: Think of `GROUP BY` as organizing data into categories.

3. **ORDER BY Clause**  
   - Sorts query results in ascending (`ASC`) or descending (`DESC`) order.
   - Syntax:  
     ```sql
     SELECT * FROM table_name ORDER BY column_name ASC|DESC;
     ```
   - Example:  
     - Ascending Order:  
       ```sql
       SELECT * FROM books ORDER BY published_date ASC;
       ```
     - Descending Order:  
       ```sql
       SELECT * FROM books ORDER BY published_date DESC;
       ```
   - **Tip**: Use `ORDER BY` to organize results chronologically, alphabetically, etc.

4. **HAVING Clause**  
   - Filters groups after aggregation (used with `GROUP BY`).
   - Unlike `WHERE`, which filters rows before grouping, `HAVING` filters after grouping.
   - Syntax:  
     ```sql
     SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING condition;
     ```
   - Example:  
     ```sql
     SELECT name, COUNT(*) FROM books GROUP BY name HAVING name LIKE '%Hack%';
     ```
   - **Tip**: Use `HAVING` when you need to filter grouped data based on conditions.


### **-----**
Imagine you’re organizing a library’s book catalog:
1. **DISTINCT**: You list all unique book titles to avoid duplicates:
   ```sql
   SELECT DISTINCT name FROM books;
   ```

2. **GROUP BY**: You count how many copies of each book you have:
   ```sql
   SELECT name, COUNT(*) FROM books GROUP BY name;
   ```

3. **ORDER BY**: You sort books by their publication date (oldest to newest):
   ```sql
   SELECT * FROM books ORDER BY published_date ASC;
   ```

4. **HAVING**: You find books with "Hack" in the title and count them:
   ```sql
   SELECT name, COUNT(*) FROM books GROUP BY name HAVING name LIKE '%Hack%';
   ```

### **Key Takeaways**
1. **DISTINCT**: Removes duplicates (`SELECT DISTINCT`).
2. **GROUP BY**: Groups data for aggregation (`COUNT`, `SUM`, etc.).
3. **ORDER BY**: Sorts results (`ASC` or `DESC`).
4. **HAVING**: Filters grouped data after aggregation.

**Tip**: Think of these clauses as tools to refine your search:
- Use `DISTINCT` to clean up duplicates.
- Use `GROUP BY` to summarize data.
- Use `ORDER BY` to sort results.
- Use `HAVING` to filter grouped data.

---
---


### **SQL Operators**


#### **1. What are Operators?**
Operators in SQL help filter and manipulate data to create precise and powerful queries. They are used to compare values, combine conditions, and test logic.


#### **2. Logical Operators**

1. **LIKE Operator**  
   - Filters data based on patterns (using `%` for wildcards).  
   - Example: Find books with "guide" in the description.  
     ```sql
     SELECT * FROM books WHERE description LIKE "%guide%";
     ```

2. **AND Operator**  
   - Combines multiple conditions; returns `TRUE` only if **all** conditions are met.  
   - Example: Find a book with a specific name and category.  
     ```sql
     SELECT * FROM books WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
     ```

3. **OR Operator**  
   - Combines multiple conditions; returns `TRUE` if **at least one** condition is met.  
   - Example: Find books with "Android" or "iOS" in the name.  
     ```sql
     SELECT * FROM books WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
     ```

4. **NOT Operator**  
   - Excludes results that match a condition.  
   - Example: Find books where the description does **not** contain "guide".  
     ```sql
     SELECT * FROM books WHERE NOT description LIKE "%guide%";
     ```

5. **BETWEEN Operator**  
   - Filters data within a specified range (inclusive).  
   - Example: Find books with IDs between 2 and 4.  
     ```sql
     SELECT * FROM books WHERE id BETWEEN 2 AND 4;
     ```

#### **3. Comparison Operators**

1. **Equal To (`=`)**  
   - Checks if two values are equal.  
   - Example: Find a book with an exact name.  
     ```sql
     SELECT * FROM books WHERE name = "Designing Secure Software";
     ```

2. **Not Equal To (`!=`)**  
   - Checks if two values are not equal.  
   - Example: Exclude books in the "Offensive Security" category.  
     ```sql
     SELECT * FROM books WHERE category != "Offensive Security";
     ```

3. **Less Than (`<`)**  
   - Checks if a value is less than another.  
   - Example: Find books published before January 1, 2020.  
     ```sql
     SELECT * FROM books WHERE published_date < "2020-01-01";
     ```

4. **Greater Than (`>`)**  
   - Checks if a value is greater than another.  
   - Example: Find books published after January 1, 2020.  
     ```sql
     SELECT * FROM books WHERE published_date > "2020-01-01";
     ```

5. **Less Than or Equal To (`<=`)**  
   - Checks if a value is less than or equal to another.  
   - Example: Find books published on or before November 15, 2021.  
     ```sql
     SELECT * FROM books WHERE published_date <= "2021-11-15";
     ```

6. **Greater Than or Equal To (`>=`)**  
   - Checks if a value is greater than or equal to another.  
   - Example: Find books published on or after November 2, 2021.  
     ```sql
     SELECT * FROM books WHERE published_date >= "2021-11-02";
     ```


### **-----**
Imagine you’re managing a bookstore’s inventory:
1. **LIKE**: You search for books with "guide" in the description:
   ```sql
   SELECT * FROM books WHERE description LIKE "%guide%";
   ```

2. **AND**: You find a specific book by name and category:
   ```sql
   SELECT * FROM books WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp";
   ```

3. **OR**: You look for books about "Android" or "iOS":
   ```sql
   SELECT * FROM books WHERE name LIKE "%Android%" OR name LIKE "%iOS%";
   ```

4. **NOT**: You exclude books with "guide" in the description:
   ```sql
   SELECT * FROM books WHERE NOT description LIKE "%guide%";
   ```

5. **BETWEEN**: You list books with IDs between 2 and 4:
   ```sql
   SELECT * FROM books WHERE id BETWEEN 2 AND 4;
   ```

6. **Comparison Operators**:  
   - Find books published before 2020:
     ```sql
     SELECT * FROM books WHERE published_date < "2020-01-01";
     ```
   - Find books published after November 2, 2021:
     ```sql
     SELECT * FROM books WHERE published_date >= "2021-11-02";
     ```


### **Key Takeaways**
1. **Logical Operators**: Use `LIKE`, `AND`, `OR`, `NOT`, and `BETWEEN` to refine your queries.
2. **Comparison Operators**: Use `=`, `!=`, `<`, `>`, `<=`, and `>=` to compare values.
3. **Best Practices**:
   - Combine operators for more complex queries.
   - Use wildcards (`%`) with `LIKE` for pattern matching.
   - Be mindful of ranges when using `BETWEEN`.


---
---


### **SQL Functions**


#### **1. What are SQL Functions?**
SQL functions help streamline queries, manipulate data, and perform calculations. They can work with strings, numbers, dates, and more.


#### **2. String Functions**

1. **CONCAT()**  
   - Combines two or more strings into one.  
   - Syntax:  
     ```sql
     CONCAT(string1, string2, ...)
     ```
   - Example: Combine book names and categories into a single description.  
     ```sql
     SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
     ```

2. **GROUP_CONCAT()**  
   - Concatenates values from multiple rows into a single string.  
   - Syntax:  
     ```sql
     GROUP_CONCAT(column_name SEPARATOR 'separator')
     ```
   - Example: Group book titles by their category.  
     ```sql
     SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books FROM books GROUP BY category;
     ```

3. **SUBSTRING()**  
   - Extracts part of a string based on position and length.  
   - Syntax:  
     ```sql
     SUBSTRING(string, start_position, length)
     ```
   - Example: Extract the year from the `published_date`.  
     ```sql
     SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
     ```

4. **LENGTH()**  
   - Returns the number of characters in a string.  
   - Syntax:  
     ```sql
     LENGTH(string)
     ```
   - Example: Find the length of book names.  
     ```sql
     SELECT LENGTH(name) AS name_length FROM books;
     ```


#### **3. Aggregate Functions**

These functions combine multiple rows into a single result.

1. **COUNT()**  
   - Counts the number of rows that match a condition.  
   - Syntax:  
     ```sql
     COUNT(*)
     ```
   - Example: Count the total number of books.  
     ```sql
     SELECT COUNT(*) AS total_books FROM books;
     ```

2. **SUM()**  
   - Adds up all the values in a column.  
   - Syntax:  
     ```sql
     SUM(column_name)
     ```
   - Example: Calculate the total price of all books.  
     ```sql
     SELECT SUM(price) AS total_price FROM books;
     ```

3. **MAX()**  
   - Finds the highest value in a column.  
   - Syntax:  
     ```sql
     MAX(column_name)
     ```
   - Example: Find the latest publication date.  
     ```sql
     SELECT MAX(published_date) AS latest_book FROM books;
     ```

4. **MIN()**  
   - Finds the lowest value in a column.  
   - Syntax:  
     ```sql
     MIN(column_name)
     ```
   - Example: Find the earliest publication date.  
     ```sql
     SELECT MIN(published_date) AS earliest_book FROM books;
     ```


### **-----**
Imagine you’re managing a bookstore’s inventory:
1. **CONCAT**: You create a summary for each book:
   ```sql
   SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
   ```

2. **GROUP_CONCAT**: You list all books grouped by their category:
   ```sql
   SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books FROM books GROUP BY category;
   ```

3. **SUBSTRING**: You extract the year from the publication date:
   ```sql
   SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
   ```

4. **LENGTH**: You check the length of each book title:
   ```sql
   SELECT LENGTH(name) AS name_length FROM books;
   ```

5. **COUNT**: You count how many books are in stock:
   ```sql
   SELECT COUNT(*) AS total_books FROM books;
   ```

6. **SUM**: You calculate the total price of all books:
   ```sql
   SELECT SUM(price) AS total_price FROM books;
   ```

7. **MAX/MIN**: You find the latest and earliest publication dates:
   ```sql
   SELECT MAX(published_date) AS latest_book, MIN(published_date) AS earliest_book FROM books;
   ```

### **Key Takeaways**
1. **String Functions**:
   - Use `CONCAT` to combine text.
   - Use `GROUP_CONCAT` to merge rows into a single string.
   - Use `SUBSTRING` to extract parts of a string.
   - Use `LENGTH` to measure string size.

2. **Aggregate Functions**:
   - Use `COUNT` to count rows.
   - Use `SUM` to add values.
   - Use `MAX`/`MIN` to find extremes.

