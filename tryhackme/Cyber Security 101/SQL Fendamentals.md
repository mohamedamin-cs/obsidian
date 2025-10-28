=![[img/Pasted image 20250910175913.png]]
                              ***SQL***                                                                      ***NoSQL***
**Relational databases** are often used when the data being stored is reliably going to be received in a consistent format, where accuracy is important, such as when processing e-commerce transactions.
**Non-relational databases**, on the other hand, are better used when the data being received can vary greatly in its format but need to be collected and organised in the same place, such as social media platforms collecting user-generated content.
![[img/Pasted image 20250910181747.png]]
Database Management System ([[DBMS]])
____
create database db_name;
show databases;
use db_name;
drop db_name;
___
CREATE TABLE example_table_name ( 
	example_column1 data_type, 
	example_column2 data_type,
	example_column3 data_type 
);
```shell-session
mysql> CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```
show tables;
DESCRIBE book_inventory; what columns are contained within a table
ALTER TABLE book_inventory 
	ADD page_count INT;
alter=change

drop table
____
CRUD = Create, Read, Update, Delete

INSERT INTO books (id, name, published_date, description) VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");
select * from book
UPDATE books SET description = "An In-Depth Guide to Android's Security Architecture." WHERE id = 1;
___
clauses : where, order by, distinct 
___
## Functions
```shell-session
mysql> SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
+------------------------------------------------------------------+
| book_info                                                         |
+------------------------------------------------------------------+
| Android Security Internals is a type of Defensive Security book. |
| Bug Bounty Bootcamp is a type of Offensive Security book.        |
| Car Hacker's Handbook is a type of Offensive Security book.      |
| Designing Secure Software is a type of Defensive Security book.  |
| Ethical Hacking is a type of Offensive Security book.            |
+------------------------------------------------------------------+

5 rows in set (0.00 sec)  
```
```shell-session
mysql> SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
    FROM books
    GROUP BY category;
+--------------------+-------------------------------------------------------------+
| category           | books                                                       |
+--------------------+-------------------------------------------------------------+
| Defensive Security | Android Security Internals, Designing Secure Software       |
| Offensive Security | Bug Bounty Bootcamp, Car Hacker's Handbook, Ethical Hacking |
+--------------------+-------------------------------------------------------------+

2 rows in set (0.01 sec)
```

```shell-session
mysql> SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
+----------------+
| published_year |
+----------------+
| 2014           |
| 2021           |
| 2016           |
| 2021           |
| 2021           |
+----------------+

5 rows in set (0.00 sec)  
```
