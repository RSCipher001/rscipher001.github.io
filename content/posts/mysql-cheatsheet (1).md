---
title: "MySQL Cheatsheet"
date: 2019-10-26T00:00:01+05:30
description: "MySQL cheatseet contains almost everything I know about MySQL, It is great resource to learn new things about MySQL"
tags: [mysql]
---

# DDL
DDL or Data Definition Language means it is used to define table and database structure, these commands are not used for BREAD/CRUD operations.

### Create Database
```sql
CREATE DATABASE <database_name>
```

### Create Table

#### Simple Table With Primary & Unique Columns
```sql
CREATE TABLE users(
    id INT UNSIGNED AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    mobile DECIMAL(10,0),

    PRIMARY KEY(id),
    CONSTRAINT UNIQUE unique_email(email),
    CONSTRAINT UNIQUE unique_mobile(mobile)
)
```

#### Simple Table With Primary & Foreign Columns
```sql
CREATE TABLE addresses(
    id INT UNSIGNED AUTO_INCREMENT,
    user_id INT UNSIGNED NOT NULL,
    address VARCHAR(255) NOT NULL,
    city VARCHAR(255),
    state VARCHAR(255),
    country VARCHAR(255) DEFAULT 'India',

    PRIMARY KEY(id),
    FOREIGN KEY(user_id) REFERENCES users(id)
        ON DELETE CASCADE
)
```

#### Table Cloning From Same Database
```sql
CREATE TABLE users_copy LIKE users
```

#### Table Cloning From Different Database with Data
For this example we are going to create table user in current database (use <database>) from clients database

```sql
CREATE TABLE users_copy SELECT * FROM clients.users
```


#### Alter Table & Add Unique
```sql
-- Unique username column in users table
ALTER TABLE users
ADD UNIQUE users_username_unique(username)
```

```sql
-- Unique Two Columns
ALTER TABLE menu
ADD CONSTRAINT unique_user_parent_id UNIQUE (id, parentId)
```

### Alter Table & Add Updated At
```sql
ALTER TABLE users
ADD COLUMN updated_at TIMESTAMP
    DEFAULT CURRENT_TIMESTAMP
    ON UPDATE CURRENT_TIMESTAMP
```

### Reset Tables With Foreign Keys
```sql
-- Disable Foreign Checks
SET FOREIGN_KEY_CHECKS = 0;

-- Truncate users Table
TRUNCATE table users;

-- Enable Foreign Checks
SET FOREIGN_KEY_CHECKS = 1;
```

### Alter Table & Add Foreign Key
```sql
-- Add foreign key to address table referencing id on users table.
ALTER TABLE addresses
ADD FOREIGN KEY (user_id) REFERENCES users(id); 
```



# DML
These commands can't change table structure but they are used for interacting with data.

### Show All Database
```sql
SHOW DATABASES
```

### Select Database
```sql
USE <database_name>
```

### Show All Tables
```sql
SHOW TABLES
```

### Show All Indexes For A Table
```sql
SHOW INDEX FROM <table_name>
```

### Insert Data
```sql
-- Alternate syntac
INSERT INTO users
    SET
        name = "Ravindra",
        email = "ravindra@example.com",
        mobile = "9876543210"
-- Mainstream syntax
INSERT INTO users
    (name, email, mobile)
    VALUES
    ("Ravindra", "ravindra@example.com", "9876543210")
```

### Insert & Update in One Query
This is useful for situation where a column (or two/more columns) are unique in table, When using insert it will create new entry but if it finds duplicate than we can run update within same query
```sql
INSERT INTO
  users
SET
  mobile = '9876543210', -- It is unique in table
  email = 'john@example.com',
-- If it already finds a record with same data (mobile = 9876543210)
ON DUPLICATE KEY UPDATE
  email = 'john@example.com' -- Just run update query
```

### UNION in MySQL

This is an example of multilevel nested menu and we are selecting id for category we want to select.
1. Select id as id
2. Select all child categories of that id and union it with our id
3. Select ids of all rows we got from last line and union with previous result.

```sql
SELECT id AS id
    UNION SELECT `id` FROM menu WHERE `parentId` = id
    UNION SELECT `id` FROM menu WHERE `parentId` IN (SELECT `id` FROM menu WHERE `parentId` = id)";
```

# Misc
Contains list about stuff that is not part of DDL or DML
### Import Data From SQL File
How to import a database, it contains both methods I know.

#### From Shell
```sql
-- Open SQL Shell and type
source path_to_sql_file.sql
```

#### From Prompt
```bash
# System Terminal/ Command Prompt
mysql -uusername -p database < sql_file.sql
```

### Enable Group By in MySQL 5.7+
Group by doesn't work in MySQL 5.7+ if column which is being used for grouping is not selected, fix that.
```sql
SET GLOBAL sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION";
```

### Add New MySQL User with All Privileges
```sql
# For localhost
CREATE USER 'ravindra'@'localhost' IDENTIFIED BY 'password';

# For all hosts
CREATE USER 'ravindra'@'%' IDENTIFIED BY 'password';

# Privilege on all database & all tables
GRANT ALL PRIVILEGES ON * . * TO 'ravindra'@'localhost';

# Privilege on shop database & all tables
GRANT ALL PRIVILEGES ON shop . * TO 'ravindra'@'localhost';
FLUSH PRIVILEGES;

# Privilege on shop database & orders tables
GRANT ALL PRIVILEGES ON shop.orders  TO 'ravindra'@'localhost';
FLUSH PRIVILEGES;
```


# DDL
DDL or Data Definition Language means it is used to define table and database structure, these commands are not used for BREAD/CRUD operations.

### Create Database
```sql
CREATE DATABASE <database_name>
```

### Create Table

#### Simple Table With Primary & Unique Columns
```sql
CREATE TABLE users(
    id INT AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255),
    mobile DECIMAL(10,0),

    PRIMARY KEY(id),
    CONSTRAINT UNIQUE unique_email(email),
    CONSTRAINT UNIQUE unique_mobile(mobile)
)
```

#### Simple Table With Primary & Foreign Columns
```sql
CREATE TABLE addresses(
    id INT AUTO_INCREMENT,
    user_id INT NOT NULL,
    address VARCHAR(255) NOT NULL,
    city VARCHAR(255),
    state VARCHAR(255),
    country VARCHAR(255) DEFAULT 'India',

    PRIMARY KEY(id),
    FOREIGN KEY(user_id) REFERENCES users(id)
        ON DELETE CASCADE
)
```

#### Table Cloning
```sql
CREATE TABLE users_copy LIKE users
```

#### Alter Table & Add Unique
```sql
-- Unique username column in users table
ALTER TABLE users
ADD UNIQUE users_username_unique(username)
```

```sql
-- Unique Two Columns
ALTER TABLE menu
ADD CONSTRAINT unique_user_parent_id UNIQUE (id, parentId)
```

### Alter Table & Add Updated At
```sql
ALTER TABLE users
ADD COLUMN updated_at TIMESTAMP
    DEFAULT CURRENT_TIMESTAMP
    ON UPDATE CURRENT_TIMESTAMP
```

### Reset Tables With Foreign Keys
```sql
-- Disable Foreign Checks
SET FOREIGN_KEY_CHECKS = 0;

-- Truncate users Table
TRUNCATE table users;

-- Enable Foreign Checks
SET FOREIGN_KEY_CHECKS = 1;
```

### Alter Table & Add Foreign Key
```sql
-- Add foreign key to address table referencing id on users table.
ALTER TABLE addresses
ADD FOREIGN KEY (user_id) REFERENCES users(id); 
```

# DML
These commands can't change table structure but they are used for interacting with data.

### Show All Database
```sql
SHOW DATABASES
```

### Select Database
```sql
USE <database_name>
```

### Show All Tables
```sql
SHOW TABLES
```

### Show All Indexes For A Table
```sql
SHOW INDEX FROM <table_name>
```

### Insert Data
```sql
-- Alternate syntac
INSERT INTO users
    SET
        name = "Ravindra",
        email = "ravindra@example.com",
        mobile = "9876543210"
-- Mainstream syntax
INSERT INTO users
    (name, email, mobile)
    VALUES
    ("Ravindra", "ravindra@example.com", "9876543210")
```

### Insert & Update in One Query
This is useful for situation where a column (or two/more columns) are unique in table, When using insert it will create new entry but if it finds duplicate than we can run update within same query
```sql
INSERT INTO
  users
SET
  mobile = '9876543210', -- It is unique in table
  email = 'john@example.com',
-- If it already finds a record with same data (mobile = 9876543210)
ON DUPLICATE KEY UPDATE
  email = 'john@example.com' -- Just run update query
```

### MySQL date between
```sql
SELECT * FROM login
WHERE (createDate BETWEEN "2019-08-03 00:00:00" AND "2019-08-05 00:00:00")

-- Another Example
SELECT * FROM login
WHERE date_format(now(),'%H:%i:%s')
    BETWEEN date_format(from_time,'%H:%i:%s') AND date_format(to_time,'%H:%i:%s') 
```

# Misc
Contains list about stuff that is not part of DDL or DML
### Import Data From SQL File
How to import a database, it contains both methods I know.

#### From Shell
```sql
-- Open SQL Shell and type
source path_to_sql_file.sql
```

#### From Prompt
```bash
# System Terminal/ Command Prompt
mysql -uusername -p database < sql_file.sql
```

### Enable Group By in MySQL 5.7+
Group by doesn't work in MySQL 5.7+ if column which is being used for grouping is not selected, fix that.
```sql
SET GLOBAL sql_mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION";
```

### Add New MySQL User with All Privileges
```sql
CREATE USER 'ravindra'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'ravindra'@'localhost';
FLUSH PRIVILEGES;
```

### Check SQL Time Zone
```sql
SELECT @@global.time_zone, @@session.time_zone;
```

### MySQL Change Time Zone
```bash
SET GLOBAL time_zone = '+5:30';
SET SESSION time_zone = '+5:30';
```

### Indexing Tips
- Hash index are best for equality based search, ex: email, mobile.
- BTREE index are best for range based search, ex: id, age & salary.
- Bitmap index are best for limited values, ex: is_active, designation.
- Indexing two columns combined can increase speed in case of where queries.
- Materialized views can be used for storing join result.
- Covering index.
- Use IS NULL.
- Don't seperate date & time.


### Mysql Cheatsheet TODO
- Collect command for horizontal, vertical partitioning.
- Collect command for creating index.
- Analyze command cheatsheet.
- Reindex command cheatsheet.
- vaccum command cheatsheet.
- Parallel exceution cheatsheet.
