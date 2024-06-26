# MySQL Connectivity with Python
# Introduction
Connecting a Python application to a MySQL database is essential for many data-driven applications. This guide provides step-by-step instructions for setting up MySQL connectivity using the mysql-connector-python library.

# Prerequisites
Python installed on your system
MySQL server running and accessible
mysql-connector-python library installed (install using pip install mysql-connector-python)
## Installation
To install the MySQL connector for Python, run:
```python
pip install mysql-connector-python
```
# Establishing a Connection
### Basic Connection Example
```python
import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(
        host='your_host',
        database='your_database',
        user='your_username',
        password='your_password'
    )

    if connection.is_connected():
        db_info = connection.get_server_info()
        print("Connected to MySQL Server version ", db_info)
        cursor = connection.cursor()
        cursor.execute("SELECT DATABASE();")
        record = cursor.fetchone()
        print("You're connected to database: ", record)

except Error as e:
    print("Error while connecting to MySQL", e)
finally:
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("MySQL connection is closed")
```

# Performing SQL Queries
### Select Query Example
```python
import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(
        host='your_host',
        database='your_database',
        user='your_username',
        password='your_password'
    )

    if connection.is_connected():
        cursor = connection.cursor()
        cursor.execute("SELECT * FROM your_table")
        records = cursor.fetchall()

        print("Total number of rows in table: ", cursor.rowcount)
        print("\nPrinting each record")
        for row in records:
            print(row)

except Error as e:
    print("Error while connecting to MySQL", e)
finally:
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("MySQL connection is closed")
```
# Inserting Data
Insert Query Example
```python
import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(
        host='your_host',
        database='your_database',
        user='your_username',
        password='your_password'
    )

    if connection.is_connected():
        cursor = connection.cursor()
        sql_insert_query = """ INSERT INTO your_table
                               (column1, column2) VALUES (%s, %s)"""
        insert_tuple = ('value1', 'value2')
        cursor.execute(sql_insert_query, insert_tuple)
        connection.commit()
        print("Record inserted successfully into your_table")

except Error as e:
    print("Failed to insert record into MySQL table {}".format(e))
finally:
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("MySQL connection is closed")
```
# Error Handling
```python
import mysql.connector
from mysql.connector import Error

try:
    connection = mysql.connector.connect(
        host='your_host',
        database='your_database',
        user='your_username',
        password='your_password'
    )

    if connection.is_connected():
        db_info = connection.get_server_info()
        print("Connected to MySQL Server version ", db_info)
        cursor = connection.cursor()
        cursor.execute("SELECT DATABASE();")
        record = cursor.fetchone()
        print("You're connected to database: ", record)

except Error as e:
    print("Error while connecting to MySQL", e)
finally:
    if connection.is_connected():
        cursor.close()
        connection.close()
        print("MySQL connection is closed")
```
# Closing the Connection
Always ensure the connection is closed after operations are completed to avoid any potential issues:

```python
if connection.is_connected():
    cursor.close()
    connection.close()
    print("MySQL connection is closed")
```
