<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SQL CrashCourse</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li>
<ul>
<li><a href="#ms-sql-a-comprehensive-guide">MS SQL: A Comprehensive Guide</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h2 id="ms-sql-a-comprehensive-guide">MS SQL: A Comprehensive Guide</h2>
<h3 id="i.-introduction-to-ms-sql-and-database-fundamentals">I. Introduction to MS SQL and Database Fundamentals</h3>
<h4 id="a.-what-is-a-database">A. What is a Database?</h4>
<p>A database is an organized collection of data, typically stored and accessed electronically from a computer system. Databases1 are designed to manage large amounts of information efficiently, allowing for easy storage, retrieval, modification, and deletion of data.</p>
<h4 id="b.-relational-database-management-systems-rdbms">B. Relational Database Management Systems (RDBMS)</h4>
<p>An RDBMS is a software system used to maintain relational databases. It provides an interface for users to interact with the database and manage the data. Microsoft SQL Server is a prominent example of an RDBMS. In an RDBMS, data is organized into tables (relations), which consist of rows and columns.</p>
<h4 id="c.-key-concepts-tables-rows-columns-primary-keys-foreign-keys">C. Key Concepts: Tables, Rows, Columns, Primary Keys, Foreign Keys</h4>
<ul>
<li><strong>Table (Relation):</strong> A table is a collection of related data organized into rows and columns. Each table represents a specific entity (e.g., “Customer,” “Loan,” “Branch”).</li>
<li><strong>Row (Record/Tuple):</strong> A single entry in a table, representing a complete set of related data for an entity. For example, in a <code>Customer</code> table, one row would contain all the information for a single customer.</li>
<li><strong>Column (Field/Attribute):</strong> A vertical entity in a table that contains all information associated with a specific field. Each column has a specific data type (e.g., text, number, date).</li>
<li><strong>Primary Key (PK):</strong> A column or a set of columns that uniquely identifies each row in a table. A primary key cannot contain NULL values and must contain unique values. It ensures data integrity and helps establish relationships with other tables.</li>
<li><strong>Foreign Key (FK):</strong> A column or a set of columns in one table that refers to the primary key in another table. The foreign key establishes a link between the two tables, enforcing referential integrity. It ensures that relationships between tables are maintained.</li>
</ul>
<h4 id="d.-data-types-brief-overview">D. Data Types (Brief overview)</h4>
<p>SQL Server supports various data types to store different kinds of information, such as:</p>
<ul>
<li><strong>Numeric:</strong> <code>INT</code>, <code>DECIMAL</code>, <code>FLOAT</code></li>
<li><strong>String:</strong> <code>VARCHAR</code>, <code>NVARCHAR</code>, <code>CHAR</code>, <code>NCHAR</code>, <code>TEXT</code>, <code>NTEXT</code></li>
<li><strong>Date and Time:</strong> <code>DATE</code>, <code>TIME</code>, <code>DATETIME</code>, <code>SMALLDATETIME</code></li>
<li><strong>Binary:</strong> <code>VARBINARY</code>, <code>BINARY</code></li>
<li><strong>Boolean:</strong> <code>BIT</code></li>
</ul>
<h3 id="ii.-database-design-and-relationships">II. Database Design and Relationships</h3>
<h4 id="a.-entity-relationship-er-model">A. Entity-Relationship (ER) Model</h4>
<p>The Entity-Relationship (ER) model is a high-level conceptual data model. It is used to represent the structure of a database graphically. It identifies entities (objects), their attributes (properties), and the relationships between these entities.</p>
<h4 id="b.-types-of-relationships">B. Types of Relationships</h4>
<p>Relationships define how data in different tables are connected.</p>
<ol>
<li>
<p>One-to-One (1:1):</p>
<p>A single record in one table is related to a single record in another table. This is less common and often indicates that the tables could be combined, but it can be useful for splitting large tables or isolating sensitive data.</p>
<ul>
<li><em>Example:</em> A <code>Person</code> table and a <code>Passport</code> table, where one person has one passport.</li>
</ul>
</li>
<li>
<p>One-to-Many (1:N):</p>
<p>A single record in one table can be related to multiple records in another table. This is the most common type of relationship.</p>
<ul>
<li><em>Example:</em> A <code>Branch</code> can have multiple <code>Loan</code>s. One <code>customer</code> can have multiple <code>account</code>s.</li>
</ul>
</li>
<li>
<p>Many-to-Many (M:N):</p>
<p>Multiple records in one table can be related to multiple records in another table. This type of relationship cannot be directly implemented in a relational database. It requires an intermediary table, often called a “linking” or “junction” table, which breaks down the many-to-many relationship into two one-to-many relationships.</p>
<ul>
<li>
<p><em>Example:</em> A <code>Customer</code> can take out many <code>Loan</code>s, and a <code>Loan</code> can be associated with many <code>Customer</code>s (via the <code>Borrower</code> table).</p>
<ul>
<li><code>Customer</code> table (CustomerID, CustomerName)</li>
<li><code>Loan</code> table (LoanNumber, Amount)</li>
<li><code>Borrower</code> (linking table) (CustomerID, LoanNumber) - where CustomerID is a foreign key to <code>Customer</code> and LoanNumber is a foreign key to <code>Loan</code>.</li>
</ul>
</li>
</ul>
</li>
</ol>
<h4 id="c.-normalization-formalization-levels">C. Normalization (Formalization Levels)</h4>
<p>Normalization is a database design technique that organizes tables in a manner that reduces data redundancy and improves data integrity. It involves a series of guidelines called normal forms.</p>
<ol>
<li>
<p><strong>1st Normal Form (1NF):</strong></p>
<ul>
<li>Each column in a table must contain atomic (indivisible) values.</li>
<li>There are no repeating groups of columns.</li>
<li>Each row is unique (typically achieved through a primary key).</li>
</ul>
</li>
<li>
<p><strong>2nd Normal Form (2NF):</strong></p>
<ul>
<li>The table must be in 1NF.</li>
<li>All non-key attributes (columns not part of the primary key) must be fully functionally dependent on the <em>entire</em> primary key. This means if the primary key is composite (made of multiple columns), no non-key attribute should depend on only part of the primary key.</li>
</ul>
</li>
<li>
<p><strong>3rd Normal Form (3NF):</strong></p>
<ul>
<li>The table must be in 2NF.</li>
<li>There are no transitive dependencies. A transitive dependency occurs when a non-key attribute is dependent on another non-key attribute.</li>
</ul>
</li>
</ol>
<h4 id="d.-functional-dependency">D. Functional Dependency</h4>
<p>A functional dependency is a constraint between two sets of attributes in a relation from a database.2 It states that if we know the value of one attribute (or a set of attributes), we can determine the value of another attribute (or set of attributes).</p>
<ul>
<li>Notation: A→B (A determines B). This means that for any given value of A, there is exactly one value of B.</li>
</ul>
<h4 id="e.-creating-databases-and-tables-based-on-azpaygah.pdf">E. Creating Databases and Tables (based on <code>azpaygah.pdf</code>)</h4>
<p>Based on <code>azpaygah.pdf</code>, you need to create a database named <code>bank</code> with several tables and then add records.</p>
<ol>
<li>
<p>CREATE DATABASE statement</p>
<p>To create a database named bank:</p>
<p>SQL</p>
<pre><code>CREATE DATABASE bank;
GO
USE bank;
GO

</code></pre>
</li>
<li>
<p>CREATE TABLE statement with constraints</p>
<p>You need to define tables with their respective columns and primary/foreign key constraints.</p>
<p>SQL</p>
<pre><code>-- Create Branch table
CREATE TABLE Branch (
    branch_name VARCHAR(50) PRIMARY KEY,
    branch_city VARCHAR(50),
    assets DECIMAL(18, 2)
);

-- Create Customer table
CREATE TABLE Customer (
    customer_name VARCHAR(50) PRIMARY KEY,
    customer_street VARCHAR(100),
    customer_city VARCHAR(50)
);

-- Create Account table
CREATE TABLE Account (
    account_number VARCHAR(50) PRIMARY KEY,
    branch_name VARCHAR(50),
    balance DECIMAL(18, 2),
    FOREIGN KEY (branch_name) REFERENCES Branch(branch_name)
);

-- Create Depositor table (linking Customer and Account)
CREATE TABLE Depositor (
    customer_name VARCHAR(50),
    account_number VARCHAR(50),
    PRIMARY KEY (customer_name, account_number),
    FOREIGN KEY (customer_name) REFERENCES Customer(customer_name),
    FOREIGN KEY (account_number) REFERENCES Account(account_number)
);

-- Create Loan table
CREATE TABLE Loan (
    loan_number VARCHAR(50) PRIMARY KEY,
    branch_name VARCHAR(50),
    amount DECIMAL(18, 2),
    FOREIGN KEY (branch_name) REFERENCES Branch(branch_name)
);

-- Create Borrower table (linking Customer and Loan)
CREATE TABLE Borrower (
    customer_name VARCHAR(50),
    loan_number VARCHAR(50),
    PRIMARY KEY (customer_name, loan_number),
    FOREIGN KEY (customer_name) REFERENCES Customer(customer_name),
    FOREIGN KEY (loan_number) REFERENCES Loan(loan_number)
);

</code></pre>
</li>
<li>
<p>Adding Records: INSERT INTO statement</p>
<p>After creating the tables, you can add sample data.</p>
<p>SQL</p>
<pre><code>-- Insert into Branch
INSERT INTO Branch (branch_name, branch_city, assets) VALUES
('Downtown', 'Brooklyn', 9000000.00),
('Redwood', 'Palo Alto', 2100000.00),
('Perryridge', 'Horseneck', 1700000.00),
('Brighton', 'Brooklyn', 7100000.00),
('Central', 'Rye', 400200.00),
('Shiraz Branch', 'Shiraz', 15000000.00);

-- Insert into Customer
INSERT INTO Customer (customer_name, customer_street, customer_city) VALUES
('John Doe', 'Main St', 'New York'),
('Jane Smith', 'Oak Ave', 'Los Angeles'),
('Alice Brown', 'Pine Ln', 'Houston'),
('Bob White', 'Cedar Rd', 'Chicago'),
('Charlie Green', 'Birch Blvd', 'Shiraz');

-- Insert into Account
INSERT INTO Account (account_number, branch_name, balance) VALUES
('A-101', 'Downtown', 500.00),
('A-215', 'Perryridge', 700.00),
('A-102', 'Brighton', 400.00),
('A-305', 'Brighton', 350.00),
('A-201', 'Central', 900.00),
('A-222', 'Redwood', 700.00),
('A-217', 'Redwood', 750.00);

-- Insert into Depositor
INSERT INTO Depositor (customer_name, account_number) VALUES
('John Doe', 'A-101'),
('Jane Smith', 'A-215'),
('Alice Brown', 'A-102'),
('Bob White', 'A-305'),
('Charlie Green', 'A-201');

-- Insert into Loan
INSERT INTO Loan (loan_number, branch_name, amount) VALUES
('L-17', 'Downtown', 1000.00),
('L-23', 'Redwood', 2000.00),
('L-15', 'Perryridge', 1500.00),
('L-14', 'Downtown', 1500.00),
('L-93', 'Brighton', 500.00),
('L-11', 'Shiraz Branch', 12000000.00),
('L-12', 'Shiraz Branch', 18000000.00),
('L-13', 'Shiraz Branch', 8000000.00),
('L-10', 'Downtown', 19000000.00);


-- Insert into Borrower
INSERT INTO Borrower (customer_name, loan_number) VALUES
('John Doe', 'L-17'),
('Jane Smith', 'L-23'),
('Alice Brown', 'L-15'),
('Bob White', 'L-93'),
('Charlie Green', 'L-11'),
('Charlie Green', 'L-12'),
('John Doe', 'L-14'),
('John Doe', 'L-10');

</code></pre>
</li>
</ol>

    </div>
  </div>
</body>

</html>
