## 65. How do you perform a SQL query using Python?


To perform a SQL query using Python, you typically need to follow these steps:

1. **Install the appropriate database connector library.**
2. **Establish a connection to the database.**
3. **Create a cursor object.**
4. **Execute the SQL query using the cursor.**
5. **Fetch the results (if applicable).**
6. **Commit changes (if applicable).**
7. **Close the cursor and connection.**

Below are examples of how to perform a SQL query using Python for different databases.

### 1. **Performing a SQL Query with SQLite**

SQLite is a lightweight, file-based database that comes pre-installed with Python. You can use the `sqlite3` module to interact with an SQLite database.

**Example:**

```python
import sqlite3

# Step 2: Establish a connection to the database
conn = sqlite3.connect('example.db')

# Step 3: Create a cursor object
cursor = conn.cursor()

# Step 4: Execute a SQL query
cursor.execute('SELECT * FROM employees')

# Step 5: Fetch the results
rows = cursor.fetchall()

# Print the results
for row in rows:
    print(row)

# Step 7: Close the cursor and connection
cursor.close()
conn.close()
```

### 2. **Performing a SQL Query with MySQL**

To interact with a MySQL database, you can use the `mysql-connector-python` library.

**Installation:**

```bash
pip install mysql-connector-python
```

**Example:**

```python
import mysql.connector

# Step 2: Establish a connection to the database
conn = mysql.connector.connect(
    host='localhost',
    user='your_username',
    password='your_password',
    database='your_database'
)

# Step 3: Create a cursor object
cursor = conn.cursor()

# Step 4: Execute a SQL query
cursor.execute('SELECT * FROM employees')

# Step 5: Fetch the results
rows = cursor.fetchall()

# Print the results
for row in rows:
    print(row)

# Step 7: Close the cursor and connection
cursor.close()
conn.close()
```

### 3. **Performing a SQL Query with PostgreSQL**

For PostgreSQL, the `psycopg2` library is commonly used.

**Installation:**

```bash
pip install psycopg2
```

**Example:**

```python
import psycopg2

# Step 2: Establish a connection to the database
conn = psycopg2.connect(
    host='localhost',
    database='your_database',
    user='your_username',
    password='your_password'
)

# Step 3: Create a cursor object
cursor = conn.cursor()

# Step 4: Execute a SQL query
cursor.execute('SELECT * FROM employees')

# Step 5: Fetch the results
rows = cursor.fetchall()

# Print the results
for row in rows:
    print(row)

# Step 7: Close the cursor and connection
cursor.close()
conn.close()
```

### General Steps to Perform a SQL Query Using Python

1. **Install the Database Driver:**
   - Use `pip` to install the appropriate database driver (e.g., `sqlite3`, `mysql-connector-python`, `psycopg2`).

2. **Establish a Connection:**
   - Use the database driver’s `connect()` function to establish a connection to the database using the appropriate credentials.

3. **Create a Cursor:**
   - Use the connection object’s `cursor()` method to create a cursor object, which is used to execute SQL queries.

4. **Execute the Query:**
   - Use the cursor’s `execute()` method to run the SQL query.

5. **Fetch the Results:**
   - If your query retrieves data (e.g., a `SELECT` statement), use `fetchone()`, `fetchall()`, or `fetchmany()` to retrieve the results.

6. **Commit Changes (if needed):**
   - If you are performing an action that modifies data (e.g., `INSERT`, `UPDATE`, `DELETE`), use the connection’s `commit()` method to save the changes.

7. **Close the Cursor and Connection:**
   - Always close the cursor and connection when you’re done to free up resources.

### Example of Inserting Data

Here’s how to insert data into a table:

```python
# Example for SQLite (similar for other databases)
cursor.execute("INSERT INTO employees (name, age, department) VALUES (?, ?, ?)", ("John Doe", 30, "HR"))
conn.commit()
```

- Use placeholders (`?` for SQLite, `%s` for MySQL/PostgreSQL) to safely insert values into SQL queries, which helps prevent SQL injection.

### Summary

Performing SQL queries in Python involves using a database-specific connector library to connect to the database, executing SQL commands using a cursor, fetching results, and properly managing the connection. The process is similar across different databases, with minor variations depending on the database driver and query syntax.