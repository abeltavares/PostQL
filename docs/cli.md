# CLI Documentation

## Installation

To install PostQL, you can use pip, the Python package installer. Open your terminal and run the following command:

```bash
pip install postql
```

This command installs PostQL and its dependencies.

## Usage

PostQL is a command-line interface for interacting with PostgreSQL databases. It allows you to connect to a database and execute SQL queries.

### Basic Usage
To start using PostQL, you need to connect to a PostgreSQL database. Use the `connect` command followed by the necessary connection parameters:

```bash
bash postql connect -H localhost -u postgres -P password -d my_database
```

This command connects to a PostgreSQL database named `my_database` on `localhost` using the user `postgres` and the password `password`.

### Commands

#### `connect`

Connects to a PostgreSQL database.

- **Options**:
  - `-H, --host`: Database host (default: `localhost`)
  - `-p, --port`: Database port (default: `5432`)
  - `-u, --user`: Database user (required)
  - `-P, --password`: Database password (required)
  - `-d, --database`: Database name (required)

#### `version`

Displays the version of PostQL.

- **Usage**:

```bash
postql -v
```

#### `help`

Displays help for PostQL.

- **Usage**:

```bash
postql -h
```

## Troubleshooting

### Common Issues

- **Connection Issues**: Ensure that the database host, port, user, and password are correct. Also, verify that the database server is running and accessible.
- **SQL Errors**: Check your SQL queries for syntax errors. PostQL will display error messages if it encounters an issue executing a query.
