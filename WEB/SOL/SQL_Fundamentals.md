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


