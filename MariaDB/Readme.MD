
Welcome!

Tips/Tricks/Notes/Commands URL Link: https://github.com/nimaxnimax/Udemy_Database

Instructor & Courses >> https://www.udemy.com/user/adrian-fischer-infotech/


MariaDB

- MariaDB is an open-source relational database management system (RDBMS).
- It was created by the original developers of MySQL, after concerns about the acquisition of MySQL by Oracle Corporation.
- MariaDB is designed as a drop-in replacement for MySQL, meaning it can function as a drop-in replacement for MySQL in most cases, while offering additional features and performance improvements.
- It supports various storage engines, including Aria, TokuDB, and InnoDB (the default storage engine for MySQL).
- MariaDB is widely used in web development, powering many popular websites and applications.
- It is compatible with MySQL in terms of syntax and database structure, making it easy for MySQL users to migrate to MariaDB.
- MariaDB is licensed under the GNU General Public License (GPL), making it free to use and distribute.
- It is known for its high performance, scalability, and reliability, making it suitable for both small-scale and enterprise-level applications.
- MariaDB is actively developed and maintained by the MariaDB Foundation and a community of developers worldwide.


Advantages of using MariaDB:

- **Open-Source:** MariaDB is open-source software, which means it is free to use and distribute. This reduces costs for businesses and developers.

- **Compatibility:** MariaDB is designed as a drop-in replacement for MySQL, so it is highly compatible with MySQL in terms of syntax and database structure. This makes it easy for MySQL users to switch to MariaDB without significant changes to their applications.

- **Performance:** MariaDB offers performance improvements over MySQL in certain scenarios, including better query optimization, enhanced storage engines, and support for more efficient indexing techniques.

- **Community Support:** MariaDB has a vibrant community of developers and users who contribute to its development, provide support, and share resources. This community-driven approach ensures rapid bug fixes, feature enhancements, and a wealth of documentation and tutorials.

- **Security:** MariaDB prioritizes security features, offering encryption at rest and in transit, user authentication mechanisms, access controls, and auditing capabilities to help protect data from unauthorized access and breaches.

- **Scalability:** MariaDB is highly scalable, capable of handling large volumes of data and high traffic loads. It supports features like parallel replication, sharding, and clustering, which enable horizontal scaling across multiple servers.

- **High Availability:** MariaDB provides features for ensuring high availability and fault tolerance, such as master-slave replication, master-master replication, and automatic failover mechanisms. These features help minimize downtime and ensure continuous access to data.

- **Extensibility:** MariaDB supports a wide range of plugins and extensions, allowing users to extend its functionality according to their specific requirements. This extensibility enables customization and integration with other software tools and platforms.

- **Active Development:** MariaDB is actively developed and maintained by the MariaDB Foundation and a large community of contributors. This ensures ongoing improvements, updates, and support for new technologies and standards.


MariaDB

To install MariaDB, you can follow these general steps. The exact commands and procedures might vary slightly depending on your operating system, so I'll provide instructions for some common ones:

**Ubuntu / Debian:**
1. Update your package index:
   ```
   sudo apt update
   ```
2. Install MariaDB server:
   ```
   sudo apt install mariadb-server
   ```
3. During the installation process, you might be prompted to set a root password for MariaDB. Follow the prompts to complete the installation.

**CentOS / Fedora:**
1. Update your package index:
   ```
   sudo yum update
   ```
2. Install MariaDB server:
   ```
   sudo yum install mariadb-server
   ```
3. Start the MariaDB service:
   ```
   sudo systemctl start mariadb
   ```
4. Enable MariaDB to start on boot:
   ```
   sudo systemctl enable mariadb
   ```

**Arch Linux:**
1. Install MariaDB:
   ```
   sudo pacman -S mariadb
   ```
2. Initialize the MariaDB data directory:
   ```
   sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
   ```
3. Start the MariaDB service:
   ```
   sudo systemctl start mariadb
   ```
4. Enable MariaDB to start on boot:
   ```
   sudo systemctl enable mariadb
   ```

Once MariaDB is installed, you can interact with it using the `mysql` command-line client to create databases, manage users, and perform other administrative tasks. For example:
```
mysql -u root -p
```
This command will prompt you for the root password you set during installation and then log you into the MariaDB command-line interface.


Example of a Bash script that connects to a MariaDB server running on Ubuntu and lists the databases:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Run the MySQL command to list databases
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "SHOW DATABASES;"
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `show_databases.sh`), make it executable using `chmod +x show_databases.sh`, and then run it using `./show_databases.sh`. It will prompt you for the password and then display the list of databases.


Example Bash script that prompts the user to input a database name, creates that database in MariaDB, and then shows the list of databases:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database to create: " DB_NAME

# Run MySQL command to create the database
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "CREATE DATABASE $DB_NAME;"

# Show the list of databases
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "SHOW DATABASES;"
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `create_and_show_databases.sh`), make it executable using `chmod +x create_and_show_databases.sh`, and then run it using `./create_and_show_databases.sh`. It will prompt you to enter a database name, create that database in MariaDB, and then display the list of databases.


Bash script that prompts the user to input a database name. If the database doesn't exist, it creates it. Then it prompts the user to input a table name and creates a sample table with that name in the specified database. Finally, it shows the list of tables in that database:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database: " DB_NAME

# Check if the database exists
DB_EXISTS=$(mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "SELECT SCHEMA_NAME FROM INFORMATION_SCHEMA.SCHEMATA WHERE SCHEMA_NAME='$DB_NAME';" -sN)

# If the database doesn't exist, create it
if [ -z "$DB_EXISTS" ]; then
    mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "CREATE DATABASE $DB_NAME;"
    echo "Database '$DB_NAME' created."
else
    echo "Database '$DB_NAME' already exists."
fi

# Prompt user for table name
read -p "Enter the name of the table: " TABLE_NAME

# Create a sample table in the specified database
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "CREATE TABLE $TABLE_NAME (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));"

echo "Table '$TABLE_NAME' created."

# Show the list of tables in the specified database
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "SHOW TABLES;"
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `create_database_and_table.sh`), make it executable using `chmod +x create_database_and_table.sh`, and then run it using `./create_database_and_table.sh`. It will prompt you to enter a database name and a table name, create the database and table if they don't exist, and then display the list of tables in the specified database.


Bash script that prompts the user to input a database name and a table name. It then creates a sample table with the provided name in the specified database and inserts 10 random usernames into the table:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database: " DB_NAME

# Prompt user for table name
read -p "Enter the name of the table: " TABLE_NAME

# Create database if it doesn't exist
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -e "CREATE DATABASE IF NOT EXISTS $DB_NAME;"
echo "Database '$DB_NAME' created or already exists."

# Create a sample table in the specified database
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "CREATE TABLE IF NOT EXISTS $TABLE_NAME (id INT AUTO_INCREMENT PRIMARY KEY, username VARCHAR(50));"
echo "Table '$TABLE_NAME' created or already exists."

# Generate 10 random usernames and insert into the table
for ((i=1; i<=10; i++))
do
    RANDOM_USERNAME=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 8 | head -n 1)
    mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "INSERT INTO $TABLE_NAME (username) VALUES ('$RANDOM_USERNAME');"
done

echo "Sample usernames inserted into the '$TABLE_NAME' table."
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `create_sample_table_and_insert_data.sh`), make it executable using `chmod +x create_sample_table_and_insert_data.sh`, and then run it using `./create_sample_table_and_insert_data.sh`. It will prompt you to enter a database name and a table name, create them if they don't exist, create a sample table, insert 10 random usernames into the table, and display appropriate messages along the way.


Bash script that prompts the user to input a database name and a table name. It then executes a `SELECT * FROM table` query on the specified table in the specified database and displays the result:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database: " DB_NAME

# Prompt user for table name
read -p "Enter the name of the table: " TABLE_NAME

# Execute SELECT * FROM table query and display result
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "SELECT * FROM $TABLE_NAME;"
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `select_from_table.sh`), make it executable using `chmod +x select_from_table.sh`, and then run it using `./select_from_table.sh`. It will prompt you to enter a database name and a table name, execute the `SELECT * FROM table` query on the specified table in the specified database, and display the result.


Bash script that prompts the user to input a database name and a table name. It then executes a `SELECT COUNT(*)` query on the specified table in the specified database to count the number of rows and displays the result:

```bash
#!/bin/bash

# MariaDB connection details
DB_USER="your_username"
DB_PASS="your_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database: " DB_NAME

# Prompt user for table name
read -p "Enter the name of the table: " TABLE_NAME

# Execute SELECT COUNT(*) FROM table query and display result
mysql -u"$DB_USER" -p"$DB_PASS" -h"$DB_HOST" -D"$DB_NAME" -e "SELECT COUNT(*) FROM $TABLE_NAME;"
```

Replace `"your_username"`, `"your_password"`, and `"localhost"` with your actual MariaDB username, password, and host if they are different.

Save this script in a file (e.g., `count_rows_in_table.sh`), make it executable using `chmod +x count_rows_in_table.sh`, and then run it using `./count_rows_in_table.sh`. It will prompt you to enter a database name and a table name, execute the `SELECT COUNT(*)` query on the specified table in the specified database, and display the result.


Bash script that prompts the user to input a database name, a username, and a password. It then creates the specified database and grants all privileges on that database to the specified user with the provided password:

```bash
#!/bin/bash

# MariaDB connection details
DB_ROOT_USER="root"
DB_ROOT_PASS="your_root_password"
DB_HOST="localhost"

# Prompt user for database name
read -p "Enter the name of the database: " DB_NAME

# Prompt user for username
read -p "Enter the username for database access: " DB_USER

# Prompt user for password
read -s -p "Enter the password for the user: " DB_USER_PASS
echo

# Create database
mysql -u"$DB_ROOT_USER" -p"$DB_ROOT_PASS" -h"$DB_HOST" -e "CREATE DATABASE IF NOT EXISTS $DB_NAME;"
echo "Database '$DB_NAME' created or already exists."

# Grant all privileges on the database to the user
mysql -u"$DB_ROOT_USER" -p"$DB_ROOT_PASS" -h"$DB_HOST" -e "GRANT ALL PRIVILEGES ON $DB_NAME.* TO '$DB_USER'@'%' IDENTIFIED BY '$DB_USER_PASS';"
echo "Privileges granted to user '$DB_USER' on database '$DB_NAME'."
```

Replace `"your_root_password"` with your actual MariaDB root password.

Save this script in a file (e.g., `create_database_and_grant_permissions.sh`), make it executable using `chmod +x create_database_and_grant_permissions.sh`, and then run it using `./create_database_and_grant_permissions.sh`. It will prompt you to enter a database name, a username, and a password. Then it will create the specified database and grant all privileges on that database to the specified user with the provided password.


MariaDB Examples

1. **Creating a Database:**
   To create a new database, you can use the `CREATE DATABASE` statement:
   ```sql
   CREATE DATABASE mydatabase;
   ```

2. **Switching to a Database:**
   To switch to a specific database, you can use the `USE` statement:
   ```sql
   USE mydatabase;
   ```

3. **Creating Tables:**
   You can create tables within a database using the `CREATE TABLE` statement:
   ```sql
   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) NOT NULL,
       email VARCHAR(100) NOT NULL
   );
   ```

4. **Inserting Data into a Table:**
   You can insert data into a table using the `INSERT INTO` statement:
   ```sql
   INSERT INTO users (username, email) VALUES ('john_doe', 'john@example.com');
   ```

5. **Querying Data:**
   To retrieve data from a table, you can use the `SELECT` statement:
   ```sql
   SELECT * FROM users;
   ```

6. **Updating Data:**
   To update existing data in a table, you can use the `UPDATE` statement:
   ```sql
   UPDATE users SET email = 'new_email@example.com' WHERE username = 'john_doe';
   ```

7. **Deleting Data:**
   To delete data from a table, you can use the `DELETE FROM` statement:
   ```sql
   DELETE FROM users WHERE username = 'john_doe';
   ```

8. **Managing Users:**
   MariaDB allows you to create and manage users for database access. For example, to create a new user:
   ```sql
   CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
   ```

9. **Granting Privileges:**
   You can grant different privileges to users for specific databases or tables. For example, to grant all privileges on a specific database to a user:
   ```sql
   GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
   ```

10. **Revoking Privileges:**
    You can also revoke previously granted privileges. For example, to revoke all privileges from a user:
    ```sql
    REVOKE ALL PRIVILEGES ON mydatabase.* FROM 'myuser'@'localhost';
    ```

11. **Creating Indexes:**
    Indexes can improve the performance of database queries. You can create indexes on one or more columns in a table using the `CREATE INDEX` statement:
    ```sql
    CREATE INDEX idx_username ON users (username);
    ```

12. **Using Joins:**
    Joins allow you to retrieve data from multiple tables based on related columns. For example, to retrieve data from two tables using an inner join:
    ```sql
    SELECT users.username, orders.order_id
    FROM users
    INNER JOIN orders ON users.id = orders.user_id;
    ```

13. **Grouping and Aggregating Data:**
    You can use the `GROUP BY` clause along with aggregate functions like `COUNT`, `SUM`, `AVG`, etc., to group and summarize data:
    ```sql
    SELECT department, COUNT(*) as num_employees
    FROM employees
    GROUP BY department;
    ```

14. **Subqueries:**
    Subqueries allow you to nest one query within another. For example, to find all users who have placed orders:
    ```sql
    SELECT username
    FROM users
    WHERE id IN (SELECT DISTINCT user_id FROM orders);
    ```

15. **Transactions:**
    MariaDB supports transactions, allowing you to execute multiple SQL statements as a single unit of work. You can use `BEGIN`, `COMMIT`, and `ROLLBACK` to manage transactions:
    ```sql
    BEGIN;
    UPDATE accounts SET balance = balance - 100 WHERE id = 123;
    UPDATE accounts SET balance = balance + 100 WHERE id = 456;
    COMMIT;
    ```

16. **Stored Procedures:**
    You can create stored procedures, which are precompiled SQL statements stored in the database and executed on demand. For example, to create a simple stored procedure:
    ```sql
    DELIMITER //
    CREATE PROCEDURE get_user_count()
    BEGIN
        SELECT COUNT(*) FROM users;
    END //
    DELIMITER ;
    ```

17. **Triggers:**
    Triggers are special stored procedures that are automatically executed in response to certain events on a table. For example, to create a trigger that updates a timestamp column when a row is inserted or updated:
    ```sql
    CREATE TRIGGER update_timestamp
    BEFORE INSERT ON orders
    FOR EACH ROW
    SET NEW.updated_at = NOW();
    ```

18. **Backing Up and Restoring Data:**
    You can use tools like `mysqldump` to create backups of your databases and `mysql` to restore them. For example, to create a backup of a database:
    ```
    mysqldump -u username -p mydatabase > backup.sql
    ```

19. **Viewing Server Status and Logs:**
    MariaDB provides various commands and tools to monitor server status and view logs, such as `SHOW STATUS`, `SHOW VARIABLES`, and viewing logs in the `/var/log/mysql/` directory.

20. **Full-Text Search:**
    MariaDB supports full-text search functionality, which allows you to perform complex searches on textual data. For example, to search for specific words within a column:
    ```sql
    SELECT * FROM articles WHERE MATCH(title, body) AGAINST('keyword');
    ```

21. **Encryption and Security:**
    MariaDB provides various features for encrypting data and enhancing security. You can encrypt data at rest and in transit, use SSL/TLS connections, and implement user authentication and access control mechanisms.

22. **Partitioning Tables:**
    Partitioning allows you to divide large tables into smaller, more manageable partitions based on specific criteria such as range, list, or hash. This can improve query performance and simplify data management:
    ```sql
    CREATE TABLE sales (
        id INT AUTO_INCREMENT PRIMARY KEY,
        sale_date DATE,
        amount DECIMAL(10, 2)
    ) PARTITION BY RANGE (YEAR(sale_date)) (
        PARTITION p0 VALUES LESS THAN (2020),
        PARTITION p1 VALUES LESS THAN (2021),
        PARTITION p2 VALUES LESS THAN MAXVALUE
    );
    ```

23. **Performance Tuning:**
    MariaDB offers various optimization techniques to improve database performance. You can analyze query execution plans, configure buffer pool size, adjust server variables, and utilize caching mechanisms to optimize performance.

24. **Replication:**
    MariaDB supports replication, allowing you to create multiple copies of a database and keep them synchronized. This can be used for load balancing, failover, and data redundancy purposes.

25. **High Availability and Clustering:**
    MariaDB supports high availability solutions such as Galera Cluster, which enables synchronous multi-master replication and automatic node synchronization. This ensures database availability and fault tolerance.

26. **Backup and Recovery Strategies:**
    In addition to basic backups, MariaDB supports advanced backup and recovery strategies such as point-in-time recovery, incremental backups, and snapshot-based backups using tools like MariaDB Backup or third-party solutions.

27. **Database Maintenance:**
    Regular database maintenance tasks include optimizing tables, monitoring server performance, analyzing query performance, and managing disk space usage. Tools like `mysqlcheck` and `mysqltuner` can assist in these tasks.

28. **Geospatial Data Handling:**
    MariaDB offers support for storing and querying geospatial data using spatial data types and spatial indexing. This enables applications to work with location-based information more effectively.

29. **User-Defined Functions (UDFs):**
    MariaDB allows you to create custom functions using different programming languages like SQL, C, or C++. These functions can extend the functionality of MariaDB and perform specialized operations.

    ```sql
    CREATE FUNCTION my_custom_function(param INT) RETURNS INT
    BEGIN
        DECLARE result INT;
        -- Custom logic here
        RETURN result;
    END;
    ```

30. **JSON Support:**
    MariaDB provides native support for storing, querying, and manipulating JSON data. You can store JSON documents in columns with the JSON data type and use functions to extract or modify JSON data.

    ```sql
    CREATE TABLE products (
        id INT PRIMARY KEY,
        details JSON
    );

    INSERT INTO products (id, details) VALUES (1, '{"name": "Product A", "price": 100}');
    SELECT details->'$.name' AS product_name FROM products WHERE id = 1;
    ```

31. **Materialized Views:**
    Materialized views are precomputed result sets stored as tables, which can improve query performance for complex or frequently accessed data. You can refresh materialized views periodically or on-demand.

    ```sql
    CREATE MATERIALIZED VIEW sales_summary AS
    SELECT DATE_FORMAT(order_date, '%Y-%m') AS month, SUM(amount) AS total_sales
    FROM orders
    GROUP BY DATE_FORMAT(order_date, '%Y-%m');

    REFRESH MATERIALIZED VIEW sales_summary;
    ```

32. **Temporal Tables:**
    Temporal tables allow you to keep track of historical changes to data by automatically recording timestamps for insertions, updates, and deletions. This can be useful for auditing or compliance purposes.

    ```sql
    CREATE TABLE employees (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100),
        salary DECIMAL(10, 2),
        valid_from DATETIME DEFAULT CURRENT_TIMESTAMP,
        valid_to DATETIME DEFAULT '9999-12-31 23:59:59'
    );

    INSERT INTO employees (name, salary) VALUES ('John Doe', 50000);
    UPDATE employees SET salary = 55000 WHERE id = 1;
    SELECT * FROM employees AS OF TIMESTAMP '2024-04-18 12:00:00';
    ```

33. **Spatial Functions:**
    MariaDB supports a variety of spatial functions for performing geometric calculations and spatial queries on geographic data. These functions enable applications to work with spatial data efficiently.

    ```sql
    SELECT ST_DISTANCE(Point(1, 1), Point(2, 2)) AS distance;
    SELECT ST_CONTAINS(Polygon((0 0, 0 10, 10 10, 10 0, 0 0)), Point(5, 5)) AS contains;
    ```

34. **Data Masking:**
    Data masking allows you to obfuscate sensitive data in query results to protect privacy and comply with data protection regulations. You can mask data using functions like `REDACT` or `MASK` to replace sensitive information with dummy values.

    ```sql
    SELECT REDACT('John Doe', 'name') AS masked_name;
    ```

35. **Window Functions:**
    Window functions allow you to perform calculations across a set of rows related to the current row. They are useful for tasks such as calculating moving averages, ranking results, or aggregating data within specific window frames.

    ```sql
    SELECT name, salary, 
           AVG(salary) OVER (PARTITION BY department) AS avg_salary_per_department
    FROM employees;
    ```

36. **Common Table Expressions (CTEs):**
    Common Table Expressions provide a way to write more readable and maintainable SQL queries by defining temporary result sets within the query. They are especially useful for complex queries or when you need to reference the same subquery multiple times.

    ```sql
    WITH high_salary_employees AS (
        SELECT * FROM employees WHERE salary > 100000
    )
    SELECT * FROM high_salary_employees;
    ```

37. **Query Optimizer Hints:**
    MariaDB allows you to provide hints to the query optimizer to influence the execution plan of a query. This can be useful when the optimizer's choices result in suboptimal performance.

    ```sql
    SELECT /*+ INDEX(users idx_username) */ * FROM users WHERE username = 'john_doe';
    ```

38. **Database Sharding:**
    Sharding involves splitting a large database into smaller, more manageable parts called shards. Each shard contains a subset of the data, allowing for horizontal scalability and improved performance.

    ```sql
    CREATE SHARD TABLE users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        username VARCHAR(50)
    ) SHARD KEY (id);
    ```

39. **Multi-Version Concurrency Control (MVCC):**
    MVCC is a technique used by MariaDB to manage concurrent access to data without locking entire tables or rows. It allows multiple transactions to read and write data simultaneously, improving concurrency and performance.

40. **Online Schema Changes:**
    MariaDB supports online schema changes, allowing you to alter tables without blocking read or write operations. This can be useful for making structural changes to your database while it is still in use.

    ```sql
    ALTER TABLE users ADD COLUMN age INT;
    ```

41. **Data Export and Import:**
    You can export data from MariaDB tables to various formats like CSV or JSON using tools like `mysqldump` or the `SELECT ... INTO OUTFILE` syntax. Similarly, you can import data from external files into MariaDB tables.

42. **Database Replication Filtering:**
    MariaDB replication filtering allows you to selectively replicate data between servers based on specific criteria, such as database, table, or row-level filtering. This can be useful for controlling which data is replicated in a multi-master setup.

