# Files

## Opening and closing files

Files can be opened using the `open()` function, which returns a file object.

It’s important to close files after use to free system resources.

```python
file = open('example.txt', 'r')
content = file.read()
print(content)
file.close()
```

We can open a file using the `with` statement, similar to working with objects.

This ensures that the file remains open only within the indented block, and it is automatically closed afterward.

```python
with open('/home/user/example.txt', 'r') as content:
    for line in content:
        print(line)
```

## Permissions

| Permission | Usage                                                                                                                    |
|------------|--------------------------------------------------------------------------------------------------------------------------|
| r          | for read only, with the pointer at the beginning of the file. It's the default                                           |
| r+         | for read and write, with the pointer at the beginning                                                                    |
| w          | for write only, overwrites the file if it exists, else creates it                                                        |
| w+         | for write and read, overwrites the file if it exists, else creates it                                                    |
| a          | for append, with the pointer at the end of the file. It creates a new file if it doesn't exist                           |
| a+         | for append and read, with the pointer at the end of the file. It creates a new file if it doesn't exist                  |
| rb         | for read only in binary format, with the pointer at the beginning                                                        |
| rb+        | for read and write in binary format, with the pointer at the beginning                                                   |
| wb         | for write only in binary format, overwrites the file if it exists, else creates it                                       |
| wb+        | for write and read in binary format, overwrites the file if it exists, else creates it                                   |
| ab         | for append in binary format, with the pointer at the end of the file. It creates a new file if it doesn't exist          |
| ab+        | for append and read in binary format, with the pointer at the end of the file. It creates a new file if it doesn't exist |

## Reading from and writing to files

### Reading a file

```python
with open('example.txt', 'r') as file:
    content = file.read()  # Reads the entire file
    print(content)
```

### Writing to a file

```python
with open('example.txt', 'w') as file:
    file.write('Hello, World!')
```

### Appending to a file

```python
with open('example.txt', 'a') as file:
    file.write('\nAppending new content')
```

## File paths and directories

Python’s `os` and `pathlib` modules help in working with file paths and directories.

Using `os`:

```python
import os

print(os.getcwd())  # Get current working directory
os.mkdir('new_directory')  # Create a new directory
```

Using `pathlib`:

```python
from pathlib import Path

path = Path('example.txt')
if path.exists():
    print('File exists!')
```

## File Object Methods: File Attributes

- `.name`: Returns the name of the file. 
- `.mode`: Returns the mode in which the file was opened. 
- `.closed`: Returns True if the file is closed, otherwise False.

Example:

```python
with open('example.txt', 'r') as file:
    print(f'File Name: {file.name}')
    print(f'File Mode: {file.mode}')
    print(f'Is Closed? {file.closed}')

print(f'Is Closed after block? {file.closed}')  # True
```

Output:

```Plain Text
File Name: example.txt
File Mode: r
Is Closed? False
Is Closed after block? True
```

## File Object Methods: Reading Methods

- `.read(size)`: Reads the entire file or a specified number of bytes. 
- `.readline()`: Reads a single line from the file. 
- `.readlines()`: Reads all lines and returns a list.

Example:

```python
with open('example.txt', 'r') as file:
    print(file.read())
    
with open('example.txt', 'r') as file:
    print(file.read(10))
    
with open('example.txt', 'r') as file:
    print(file.readline())
    
with open('example.txt', 'r') as file:
    print(file.readlines())
```

Output:

```Plain Text
Hello World, this is an example file.
Second line.

Hello Worl

Hello World, this is an example file.

['Hello World, this is an example file.\n', 'Second line.\n']
```

## File Object Methods: Writing Methods

- `.write(string)`: Writes a string to the file.
- `.writelines(iterable)`: Writes multiple lines from an iterable.

Example:

```python
with open('output.txt', 'w') as file:
    file.write('First line\n')
    file.writelines(['Second line\n', 'Third line\n'])
```

## Error Handling

Errors may occur when working with files, such as trying to read a non-existent file.

Using exception handling (try-except) prevents crashes.

```python
try:
    with open('non_existent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print('Error: File not found!')
except PermissionError:
    print('Error: No permission to access the file!')
```

## Pickle

The `pickle` module allows serializing Python objects in a file, preserving their structure for later retrieval and deserialization.

Example of serializing:

```python
import pickle

data = {'name': 'Daniel', 'age': 24, 'city': 'Madrid'}

with open('data.pkl', 'wb') as file:
    pickle.dump(data, file) 
```

Example of deserializing:

```python
with open('data.pkl', 'rb') as file:
    loaded_data = pickle.load(file)

print(loaded_data)
```

Output:

```Plain Text
{'name': 'Daniel', 'age': 24, 'city': 'Madrid'}
```

Always use binary mode (`wb` / `rb`) when working with pickle.

Only works within Python, cannot be directly deserialized by other languages.

Be cautious when deserializing untrusted data, as it can execute arbitrary code.

## Shelve

The `shelve` module provides a way to store and retrieve Python objects like a dictionary.

It uses `pickle` internally but offers key-value access.

Example of storing data:

```python
import shelve

with shelve.open('storage.db') as db:
    db['user'] = {'name': 'Daniel', 'age': 24}
    db['settings'] = {'theme': 'dark', 'language': 'EN'}
```

Example of retrieving data:

```python
with shelve.open('storage.db') as db:
    print(db['user'])
    print(db.get('settings', {}))
```

Output:

```Plain Text
{'name': 'Daniel', 'age': 30}
{'theme': 'dark', 'language': 'EN'}
```

Works like a `dictionary` but persists between executions.

Automatically handles file storage without needing explicit serialization.

Supports only string keys; values can be any serializable object.
