# SQLite3

## Connecting to an SQLite database

SQLite3 is a lightweight database that doesn’t require server processes and allows accessing the database using a variant of SQL.

You can connect to an SQLite database using the `sqlite3` module.

If the database does not exist, it will be created automatically.

Example:

```python
import sqlite3

conn = sqlite3.connect('example.db')

conn.close()
```

Always close the connection when done.

## Creating tables and inserting data

SQLite3 uses cursors to interact with the database.

A cursor is an object used to execute SQL queries and fetch results from a SQLite database.

Example of creating a table:

```python
cursor.execute('''
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY,
        name TEXT,
        age INTEGER
    )
''')
conn.commit()
```

Example of inserting a row and return its index:

```python
cursor.execute('''
    INSERT INTO users (name, age)
    VALUES (?, ?)
''', ('Daniel', 24))
conn.commit()

row_id = cursor.lastrowid
```

Example of inserting multiple rows:

```python
users = [('Daniel', 24), ('Álex', 23)]
cursor.executemany('''
    INSERT INTO users (name, age)
    VALUES (?, ?)
''', users)

conn.commit()
```

## Querying the database

Example of fetching all data:

```python
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()

for row in rows:
    print(row)
```

Output:

```Plain Text
(1, 'Daniel', 24)
(2, 'Álex', 23)
```

Example of fetching a single row:

```python
user_id = 1

cursor.execute('SELECT * FROM users WHERE id = ?', (user_id,))
row = cursor.fetchone()
print(row)
```

Output:

```Plain Text
(1, 'Daniel', 24)
```

## Handling transactions

SQLite supports transactions that allow multiple operations to be executed as a single unit.

You can use `commit()` to save the changes or `rollback()` to revert them.

## Error Handling

SQLite operations may raise exceptions, and it is important to handle errors appropriately.

Examples:

```python
try:
    cursor.execute('SELECT * FROM non_existent_table')
except sqlite3.DatabaseError as e:
    print(f'Database error occurred: {e}')
```

```python
try:
    cursor.execute('INSERT INTO users (id, name, age) VALUES (?, ?)', (1, 'Daniel', 24))
    cursor.execute('INSERT INTO users (id, name, age) VALUES (?, ?)', (1, 'Álex', 23))
    conn.commit()
except sqlite3.IntegrityError as e:
    print(f'Integrity error occurred: {e}')
```