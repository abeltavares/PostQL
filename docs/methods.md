# Methods Description

[Creating a PostgreSQL Instance](#creating-a-postgresql-instance)
- [Database Management Methods](#database-management-methods)
    - [connect (database)](#connectdatabase)
    - [disconnect ()](#disconnect)
    - [create_database (new_database)](#create_databasenew_database)
    - [delete_database (database_to_delete)](#delete_databasedatabase_to_delete)
    - [create_user (username, password, is_superuser)](#create_userusername-password-is_superuser)
    - [delete_user (username)](#delete_userusername)
    - [create_table (name, schema)](#create_tablename-schema)
    - [drop_table (name)](#drop_tablename)
    - [get_table_schema (table)](#get_table_schematable)
    - [get_connection_details ()](#get_connection_details)
<br>

- [Data Operations Methods](#data-operations-methods)
    - [select (table, columns=None)](#selecttable-columnsnone)
    - [insert (table, data)](#inserttable-data)
    - [update (table)](#updatetable)
    - [set (data)](#setdata)
    - [delete (table)](#deletetable)
    - [join (table, join_type="INNER")](#jointable-join_typeinner)
    - [on (condition)](#oncondition)
    - [where (conditions)](#whereconditions)
    - [order (columns, asc=False)](#ordercolumns-ascfalse)
    - [groupby (columns)](#groupbycolumns)
    - [limit (limit_value)](#limitlimit_value)
    - [execute ()](#execute)
    - [sql (query)](#sqlquery)


    - *Data Exportation*
        - [to_csv (output_file)](#to_csvoutput_file)
        - [to_excel (output_file)](#to_exceloutput_file)
        - [to_json (output_file)](#to_jsonoutput_file)
        - [to_parquet (output_file)](#to_parquetoutput_file)
        - [upload_to_s3 (bucket_name, format, filename, acl=None, metadata=None)](#upload_to_s3bucket_name-format-filename-aclnone-metadatanone)

<br>

### Creating a PostgreSQL Instance

Before you can perform any database management or data operations, you need to create an instance of the `Postgres` class. This instance represents a connection to a PostgreSQL database.

To create a PostgreSQL instance, you need to provide the connection details such as the host, port, user, and password. 

```python
db = Postgres( host="localhost", port="5432", user="my_user", password="my_password")
```

### Database Management Methods

#### `connect(database)`

The `connect` method establishes a connection to the PostgreSQL server.

#### Parameters

- `database` (str): The name of the database to connect to.

#### Returns

- None

#### Example

```python
db.connect(database="my_database")
```

#### Error Handling
If an error occurs during the connection process, such as an authentication failure or a database connection issue, the method catches the `psycopg2.Error` exception, logs an error message, and re-raises the exception.

#### Use Case
Connecting to a database is a fundamental operation when working with PostgreSQL. This method is used to establish a connection to a database before performing any database management or data operations.

#### `disconnect()`

The `disconnect` method closes the current database connection.

#### Parameters

- None

#### Returns

- None

#### Example

```python
db.disconnect()
```

#### Error Handling
The method does not explicitly handle errors during the disconnection process, as the `psycopg2` library's `close` method does not typically raise exceptions for errors that occur during the disconnection process.

#### Use Case
Disconnecting from a database is important for freeing up resources and ensuring that the database connection is properly closed when it is no longer needed.

#### `create_database(new_database)`

The `create_database` method creates a new database.

#### Parameters

- `new_database` (str): The name of the database to create.

#### Returns

- None

#### Example

```python
db.create_database("new_database")
```

#### Error Handling
If an error occurs during the database creation process, such as a syntax error in the SQL query or a permission issue, the method logs an error message and re-raises the exception.

#### Use Case
Creating a new database is a common operation when setting up a new PostgreSQL environment or when creating a new database for a specific application.

### `delete_database(database_to_delete)`

The `delete_database` method deletes a specified database.

#### Parameters

-   `database_to_delete` (str): The name of the database to delete.

#### Returns

-   None

#### Example

`db.delete_database("database_to_delete")`

#### Error Handling

If an error occurs during the database deletion process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Deleting a database is a common operation when cleaning up old or unused databases, especially in development or testing environments.

### `create_user(username, password, is_superuser)`

The `create_user` method creates a new user with the specified username and password.

#### Parameters

-   `username` (str): The username of the new user.
-   `password` (str): The password for the new user.
-   `is_superuser` (bool, optional): Whether the new user should be a superuser. Defaults to `False`.

#### Returns

-   None

#### Example

`db.create_user("new_user", "new_password", is_superuser=True)`

#### Error Handling

If an error occurs during the user creation process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Creating new users is a common operation when setting up a new PostgreSQL environment or when adding new users for specific applications or services.

### `delete_user(username)`

The `delete_user` method deletes a specified user.

#### Parameters

-   `username` (str): The username of the user to delete.

#### Returns

-   None

#### Example

`db.delete_user("user_to_delete")`

#### Error Handling

If an error occurs during the user deletion process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Deleting users is a common operation when cleaning up old or unused users, especially in development or testing environments.

### `create_table(name, schema)`

The `create_table` method creates a new table with the specified name and schema.

#### Parameters

-   `name` (str): The name of the new table.
-   `schema` (dict): A dictionary representing the schema of the new table, where keys are column names and values are data types.

#### Returns

-   None

#### Example

`db.create_table("new_table", {"id": "SERIAL PRIMARY KEY", "name": "VARCHAR(255)"})`

#### Error Handling

If an error occurs during the table creation process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Creating new tables is a common operation when setting up a new PostgreSQL environment or when adding new tables for specific applications or services.

### `drop_table(name)`

The `drop_table` method drops a specified table.

#### Parameters

-   `name` (str): The name of the table to drop.

#### Returns

-   None

#### Example

`db.drop_table("table_to_drop")`

#### Error Handling

If an error occurs during the table dropping process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Dropping tables is a common operation when cleaning up old or unused tables, especially in development or testing environments.

### `get_table_schema(table)`

The `get_table_schema` method retrieves and prints the schema of a specified table.

#### Parameters

-   `table` (str): The name of the table to retrieve the schema for.

#### Returns

-   None

#### Example

`db.get_table_schema("my_table")`

#### Error Handling

If an error occurs during the schema retrieval process, such as a syntax error in the SQL query or a permission issue, the method logs an error message and re-raises the exception.

#### Use Case

Retrieving the schema of a table is useful for understanding the structure of the table and for planning database migrations or schema changes.

### `get_connection_details()`

The `get_connection_details` method retrieves the connection details.

#### Parameters

-   None

#### Returns

-   None

#### Example

`db.get_connection_details()`

#### Error Handling

The method does not explicitly handle errors, as it simply logs the connection details.

#### Use Case

Retrieving connection details is useful for troubleshooting and for verifying that the correct database and user are being used.

This documentation provides a comprehensive guide to using the `DatabaseManagement` class for managing PostgreSQL databases and users. It includes detailed descriptions of each method, along with examples of how to use them.

### Data Operations Methods

### `select(table, columns=None)`

The `select` method constructs a SELECT SQL query.

#### Parameters

-   `table` (str): The name of the table to select from.
-   `columns` (list, optional): A list of column names to select. Defaults to `None`, which selects all columns.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.select("my_table", ["column1", "column2"])`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Selecting data from a table is a fundamental operation when working with PostgreSQL. This method is used to construct a SELECT query, which can be further refined with additional clauses like WHERE, JOIN, etc.

### `insert(table, data)`

The `insert` method constructs an INSERT SQL query.

#### Parameters

-   `table` (str): The name of the table to insert into.
-   `data` (dict): A dictionary where keys are column names and values are the corresponding values to insert.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.insert("my_table", {"column1": "value1", "column2": "value2"})`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Inserting data into a table is a common operation when working with PostgreSQL. This method is used to construct an INSERT query.

### `update(table)`

The `update` method starts the construction of an UPDATE SQL query.

#### Parameters

-   `table` (str): The name of the table to update.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.update("my_table")`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Updating data in a table is a common operation when working with PostgreSQL. This method is used to start the construction of an UPDATE query, which can be further refined with SET and WHERE clauses.

### `set(data)`

The `set` method adds a SET clause to an UPDATE SQL query.

#### Parameters

-   `data` (dict): A dictionary where keys are column names and values are the corresponding values to set.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.update("my_table").set({"column1": "new_value1", "column2": "new_value2"})`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Setting new values for columns in an UPDATE query is a common operation when working with PostgreSQL. This method is used to add a SET clause to an UPDATE query.

### `delete(table)`

The `delete` method constructs a DELETE SQL query.

#### Parameters

-   `table` (str): The name of the table to delete from.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.delete("my_table")`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Deleting data from a table is a common operation when working with PostgreSQL. This method is used to construct a DELETE query, which can be further refined with a WHERE clause.

### `join(table, join_type="INNER")`

The `join` method adds a JOIN clause to a SQL query.

#### Parameters

-   `table` (str): The name of the table to join with.
-   `join_type` (str, optional): The type of join to perform. Defaults to `"INNER"`.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.join("another_table", "LEFT")`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Joining tables is a common operation when working with PostgreSQL. This method is used to add a JOIN clause to a query, which can be further refined with an ON clause.

### `on(condition)`

The `on` method adds an ON clause to a JOIN SQL query.

#### Parameters

-   `condition` (str): The condition for the join.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.on("my_table.id = another_table.id")`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Specifying the condition for a join is a common operation when working with PostgreSQL. This method is used to add an ON clause to a JOIN query.

### `where(conditions)`

The `where` method adds a WHERE clause to a SQL query.

#### Parameters

-   `conditions` (dict): A dictionary where keys are column names and values are the corresponding values to match.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.where({"column1": "value1", "column2": ("<", "value2")})`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Filtering rows in a query is a common operation when working with PostgreSQL. This method is used to add a WHERE clause to a query.

### `order(columns, asc=False)`

The `order` method adds an ORDER BY clause to a SQL query.

#### Parameters

-   `columns` (list): A list of column names to order by.
-   `asc` (bool, optional): Whether to order in ascending order. Defaults to `False`, which orders in descending order.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.order(["column1", "column2"], asc=True)`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Ordering rows in a query is a common operation when working with PostgreSQL. This method is used to add an ORDER BY clause to a query.

### `groupby(columns)`

The `groupby` method adds a GROUP BY clause to a SQL query.

#### Parameters

-   `columns` (list): A list of column names to group by.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.groupby(["column1", "column2"])`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Grouping rows in a query is a common operation when working with PostgreSQL. This method is used to add a GROUP BY clause to a query.

### `limit(limit_value)`

The `limit` method adds a LIMIT clause to a SQL query.

#### Parameters

-   `limit_value` (int): The maximum number of rows to return.

#### Returns

-   `self`: Returns the instance to allow method chaining.

#### Example

`db.limit(10)`

#### Error Handling

This method does not explicitly handle errors. Errors in the SQL query construction or execution are handled by the `execute` method.

#### Use Case

Limiting the number of rows returned in a query is a common operation when working with PostgreSQL. This method is used to add a LIMIT clause to a query.

### `execute()`

The `execute` method executes the constructed SQL query.

#### Parameters

-   None

#### Returns

-   None

#### Example

`db.execute()`

#### Error Handling

If an error occurs during the query execution process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Executing a constructed SQL query is a fundamental operation when working with PostgreSQL. This method is used to execute the query that has been constructed with the previous methods.

### `sql(query)`

The `sql` method executes a raw SQL query.

#### Parameters

-   `query` (str): The raw SQL query to execute.

#### Returns

-   `result, columns`: If the query returns results, returns the results and the column names. Otherwise, returns `True`.

#### Example

`db.sql("SELECT * FROM my_table")`

#### Error Handling

If an error occurs during the query execution process, such as a syntax error in the SQL query or a permission issue, the method logs an error message.

#### Use Case

Executing raw SQL queries is useful for operations that cannot be easily constructed with the provided methods. This method is used to execute any SQL query.

#### `to_csv(output_file)`

Exports the query results to a CSV file.

##### Parameters

-   `output_file` (str, optional): The name of the output CSV file. Defaults to `"output.csv"`.

##### Returns

-   None

##### Example

`db.select(table="users", columns=["name", "age"]).where({'age': ('>',25)}).order(["age"], asc=True).limit(3).to_csv("user_results.csv")`

##### Error Handling

If an error occurs during the export process, such as a file write error, the method logs an error message.

##### Use Case

Exporting query results to a CSV file is useful for data analysis and reporting. This method is used to export the results of a query to a CSV file, which can then be easily imported into other tools or applications.

#### `to_excel(output_file)`

Exports the query results to an Excel file.

##### Parameters

-   `output_file` (str, optional): The name of the output Excel file. Defaults to `"output.xlsx"`.

##### Returns

-   None

##### Example

`db.select(table="users", columns=["name", "age"]).where({'age': ('>',25)}).order(["age"], asc=True).limit(3).to_excel("user_results.xlsx")`

##### Error Handling

If an error occurs during the export process, such as a file write error, the method logs an error message.

##### Use Case

Exporting query results to an Excel file is useful for data analysis and reporting. This method is used to export the results of a query to an Excel file, which can then be easily imported into other tools or applications.

#### `to_json(output_file)`

Exports the query results to a JSON file.

##### Parameters

-   `output_file` (str, optional): The name of the output JSON file. Defaults to `"output.json"`.

##### Returns

-   None

##### Example

`db.select(table="users", columns=["name", "age"]).where({'age': ('>',25)}).order(["age"], asc=True).limit(3).to_json("user_results.json")`

##### Error Handling

If an error occurs during the export process, such as a file write error, the method logs an error message.

##### Use Case

Exporting query results to a JSON file is useful for data analysis and reporting. This method is used to export the results of a query to a JSON file, which can then be easily imported into other tools or applications.

#### `to_parquet(output_file)`

Exports the query results to a Parquet file.

##### Parameters

-   `output_file` (str, optional): The name of the output Parquet file. Defaults to `"output.parquet"`.

##### Returns

-   None

##### Example

`db.select(table="users", columns=["name", "age"]).where({'age': ('>',25)}).order(["age"], asc=True).limit(3).to_parquet("user_results.parquet")`

##### Error Handling

If an error occurs during the export process, such as a file write error, the method logs an error message.

##### Use Case

Exporting query results to a Parquet file is useful for data analysis and reporting. This method is used to export the results of a query to a Parquet file, which can then be easily imported into other tools or applications.

#### `upload_to_s3(bucket_name, format, filename, acl=None, metadata=None)`

Uploads the exported file to an Amazon S3 bucket.

##### Parameters

-   `bucket_name` (str): The name of the S3 bucket to upload to.
-   `format` (str): The format of the exported file (e.g., "csv", "excel", "json", "parquet").
-   `filename` (str): The name of the exported file.
-   `acl` (str, optional): The access control list (ACL) setting for the uploaded file. Defaults to `None`.
-   `metadata` (dict, optional): Metadata to associate with the uploaded file. Defaults to `None`.

##### Returns

-   None

##### Example

`db.select(table="users", columns=["name", "age"]).where({'age': ('>',25)}).order(["age"], asc=True).limit(3).to_parquet("user_results.parquet").upload_to_s3("my_data_bucket", "parquet", "user_results.parquet")`

##### Error Handling

If an error occurs during the upload process, such as an S3 access error, the method logs an error message.

##### Use Case

Uploading exported files to Amazon S3 is useful for storing and sharing data. This method is used to upload the exported file to an S3 bucket, making it accessible for further analysis or sharing.
