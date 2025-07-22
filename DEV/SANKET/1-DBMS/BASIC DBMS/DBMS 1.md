---
view-count: 3
---
Before the advent of **Database Management Systems (DBMS)**, data was stored and managed using **file systems**

### **File-Based Systems**

- **Storage Mediums**: Data was stored on physical media such as punched cards, magnetic tapes, and later on, hard drives.
- **File Organization**: Data was organized in files, often in plain text or binary format.
- **Custom Programs**: Each application had its own custom code to handle data storage and retrieval.
- **Data Duplication**: Data was often duplicated across files, leading to redundancy.
- **Lack of Standardization**: There were no universal standards for managing data


### **Challenges of File-Based Systems**

1. **Data Redundancy**:
    - Same data stored in multiple places caused inconsistencies.
2. **Data Inconsistency**:
    - Changes in one file were not reflected in others.
3. **No Data Integrity**:
    - No mechanisms to enforce rules like unique IDs or relationships between records.
4. **Limited Accessibility**:
    - Data could not be easily shared between programs or systems.
5. **No Query Mechanism**:
    - Complex operations required extensive custom programming.
6. **Concurrency Issues**:
    - Multiple users accessing and updating the same data simultaneously led to errors.
7. **Poor Security**:
    - Data security depended entirely on the operating system and was often inadequate.


## DATABASES

A **database** is an organized collection of data that is stored, managed, and accessed electronically. It allows for efficient data storage, retrieval, and manipulation while ensuring consistency and security.

### **Key Features of Databases**

1. **Structured Data Storage**:
    
    - Data is organized into tables, rows, and columns in a relational database or in other formats like key-value pairs, documents, or graphs in non-relational databases.
2. **Efficient Data Management**:
    
    - Databases use specialized software called **Database Management Systems (DBMS)** to handle storage, retrieval, and manipulation.
3. **Data Relationships**:
    
    - Databases allow relationships to be established between different pieces of data (e.g., customers and their orders).
4. **Query Language**:
    
    - They often use languages like **SQL (Structured Query Language)** for querying and updating the data.
5. **Concurrency and Transactions**:
    
    - Support for multiple users accessing and modifying data simultaneously while maintaining consistency through transaction management.
6. **Data Integrity and Constraints**:
    
    - Ensure that the data remains accurate and adheres to predefined rules.
7. **Security**:
    
    - Databases provide mechanisms for user authentication, authorization, and encryption to protect sensitive data.

### **Types of Databases**

1. **Relational Databases** (RDBMS):
    
    - Store data in tables with predefined relationships.
    - Examples: MySQL, PostgreSQL, Oracle Database, SQL Server.
2. **NoSQL Databases**:
    
    - Designed for unstructured or semi-structured data.
    - Types include:
        - Key-Value Databases (e.g., Redis)
        - Document Databases (e.g., MongoDB)
        - Columnar Databases (e.g., Cassandra)
        - Graph Databases (e.g., Neo4j)
3. **Hierarchical Databases**:
    
    - Organize data in a tree-like structure.
    - Example: IBM IMS.
4. **Network Databases**:
    
    - Use a graph structure to represent relationships.
    - Example: CODASYL DBTG.
5. **Object-Oriented Databases**:
    
    - Store data as objects, similar to object-oriented programming.
    - Example: ObjectDB.
6. **In-Memory Databases**:
    
    - Store data in the system's memory for faster access.
    - Example: SAP HANA.
7. **Distributed Databases**:
    
    - Data is spread across multiple locations or systems.
    - Example: Google Spanner.






## Database Management System (DBMS)

A **Database Management System (DBMS)** is software that enables users to create, manage, and interact with databases. It acts as an intermediary between users and the database, allowing data to be stored, retrieved, and manipulated efficiently while ensuring security, integrity, and consistency.

### **Key Features of DBMS**

1. **Data Storage and Retrieval**:
    
    - Provides mechanisms to store large volumes of data and retrieve it efficiently.
2. **Data Abstraction**:
    
    - Hides the complexities of data storage from the user and presents it in a user-friendly format.
3. **Data Independence**:
    
    - Changes in the database structure do not affect application programs.
4. **Data Security**:
    
    - Offers features like user authentication, access control, and encryption to protect sensitive data.
5. **Concurrency Control**:
    
    - Ensures multiple users can access and modify the database simultaneously without conflicts.
6. **Data Integrity**:
    
    - Maintains accuracy and consistency of data through constraints (e.g., unique, primary keys, foreign keys).
7. **Backup and Recovery**:
    
    - Protects against data loss by enabling data recovery mechanisms.
8. **Query Processing**:
    
    - Provides a query language like SQL to interact with the database. 


### **Advantages of DBMS**

1. Reduces data redundancy.
2. Ensures data consistency and accuracy.
3. Simplifies data management.
4. Provides scalability for large datasets.
5. Supports complex queries and analytics.
6. Facilitates data sharing and collaboration.




### **Components of a DBMS**

1. **Database**:
    
    - The organized collection of data managed by the DBMS.
2. **Database Engine**:
    
    - Handles data storage, retrieval, and updates.
3. **Query Processor**:
    
    - Interprets and executes user queries.
4. **Schema Manager**:
    
    - Manages database structure (schemas) and metadata.
5. **Transaction Manager**:
    
    - Ensures atomicity, consistency, isolation, and durability (ACID properties) for database transactions.


### **Types of DBMS**

1. **Relational DBMS (RDBMS)**:
    
    - Stores data in tables with rows and columns.
    - Example: MySQL, PostgreSQL, Oracle Database.

![615](../../../Images/DBMS%201-20241224100514333.webp)
All RDBMS are kinda same since they follow the same SQL STANDARDS



2. **NoSQL DBMS**:
    
    - Handles unstructured or semi-structured data.
    - Example: MongoDB, Cassandra.
3. **Hierarchical DBMS**:
    
    - Organizes data in a tree-like structure.
    - Example: IBM IMS.
4. **Network DBMS**:
    
    - Represents data as records connected by links.
    - Example: Integrated Data Store (IDS).
5. **Object-Oriented DBMS**:
    
    - Integrates object-oriented programming concepts with databases.
    - Example: ObjectDB.



## SQL
**SQL (Structured Query Language)** is a standardized programming language used to manage and interact with relational databases. It is designed to perform tasks such as querying, updating, and managing data and database structures.

### **Key Features of SQL**

1. **Declarative Language**:
    
    - You specify **what** you want to do with the data (e.g., retrieve or update), not **how** it should be done.
2. **Standardized**:
    
    - SQL is governed by standards like **ANSI** and **ISO**, ensuring compatibility across most relational database systems.
3. **Data Manipulation and Management**:
    
    - SQL enables users to query, insert, update, delete, and manage data efficiently.
4. **Platform Independence**:
    
    - While SQL syntax may vary slightly between database systems (e.g., MySQL, PostgreSQL, SQL Server), the core language is universal.

**Not all DBMS (Database Management Systems) support the exact same SQL syntax or instructions.** This can be confusing, especially when switching between different systems like MySQL, PostgreSQL, Oracle, or SQL Server.
### **Why Do DBMS Differ in SQL Syntax?**

**Unique Features**:

- Each DBMS is designed with specific goals, and they introduce proprietary syntax for advanced features:
    - **MySQL**: Focuses on speed and simplicity; some advanced features are simplified or omitted (e.g., no direct `FULL OUTER JOIN`).
    - **PostgreSQL**: Emphasizes standards compliance and advanced functionality, like support for `FULL OUTER JOIN` and window functions.
    - **Oracle**: Adds enterprise-level features for scalability, security, and transactions, with its own SQL extensions.
    - **SQL Server**: Tailors its SQL (T-SQL) for tight integration with Microsoft's ecosystem.

While the **core SQL commands** (like `SELECT`, `INSERT`, `UPDATE`, `DELETE`) are standardized, each DBMS often extends these standards with custom features and syntax to provide additional functionality.


### **Examples of SQL Syntax Differences**

|**Feature**|**MySQL Syntax**|**PostgreSQL Syntax**|**Oracle Syntax**|
|---|---|---|---|
|Full Outer Join|`LEFT JOIN ... UNION RIGHT JOIN`|`FULL OUTER JOIN`|`FULL OUTER JOIN`|
|String Concatenation|`CONCAT('A', 'B')`|`'A'||
|Limit Rows|`LIMIT 10 OFFSET 5`|`LIMIT 10 OFFSET 5`|`FETCH FIRST 10 ROWS ONLY OFFSET 5`|
|Auto-Increment Column|`AUTO_INCREMENT`|`SERIAL`|`GENERATED AS IDENTITY`|
|Current Date/Time|`NOW()`|`CURRENT_TIMESTAMP`|`SYSDATE`|

- **Check Documentation**:
    
    - Refer to the official documentation for the DBMS you are using.
- **Use Standard SQL Where Possible**:
    
    - Stick to ANSI-standard SQL commands to ensure portability.
- **Adopt DBMS-Specific Syntax When Needed**:
    
    - For advanced features, learn and use the specific syntax for your DBMS.
- **Database Abstraction Tools**:
    
    - Use libraries like **SQLAlchemy** (Python) or **Hibernate** (Java), which abstract database operations and handle syntax differences automatically.


## MYSQL
**MySQL is a DBMS**, specifically a **Relational Database Management System (RDBMS)**. It is one of the most popular database systems used for managing structured data stored in tables with rows and columns.

When you run MySQL, a **server process** is set up. This server, known as the **MySQL Server**, is responsible for managing the database, processing queries, and handling requests from clients.

### **How the MySQL Server Works**

1. **Server Setup**:
    
    - When you start MySQL, a server instance is initialized.
    - This server listens for incoming connections on a specified port (default is **3306**) and manages the underlying database files.
2. **Client-Server Architecture**:
    
    - MySQL follows a client-server model.
    - The **server** handles all database operations, while **clients** connect to it to interact with the database using SQL commands.
3. **What Happens When the Server Runs**:
    
    - The MySQL server:
        - Loads the databases from storage.
        - Starts listening for client connections (local or remote).
        - Processes incoming SQL queries (like `SELECT`, `INSERT`, etc.).
        - Sends the results of the queries back to the client.
4. **Multi-User Access**:
    
    - The server allows multiple clients to connect simultaneously, enabling concurrent operations.



