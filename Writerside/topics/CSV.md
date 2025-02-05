# CSV

## Reading CSV files

The `csv` module allows for reading CSV files in a simple and efficient manner.

You can read each row as a `list` or as a `dictionary`, depending on your needs.

Example of reading as `list`:

```python
import csv

with open('example.csv', 'r') as file:
    csv_reader = csv.reader(file)
    for row in csv_reader:
        print(row)
```

Output:

```Plain Text
['name', 'age', 'city']
['Daniel', '24', 'Madrid']
```

Example of reading as `dict`:

```python
with open('example.csv', 'r') as file:
    csv_dict_reader = csv.DictReader(file)
    for row in csv_dict_reader:
        print(row)
```

Output:

```Plain Text
{'name': 'Daniel', 'age': '24', 'city': 'Madrid'}
```

## Writing to CSV files

You can write data to CSV files by using `.writer()` for a list or `.DictWriter()` for dictionaries.

Example of writing as `list`:

```python
import csv

data = [['Name', 'Age', 'City'], ['Daniel', 24, 'Madrid'], ['Álex', 23, 'Gijón']]

with open('output.csv', 'w', newline='') as file:
    csv_writer = csv.writer(file)
    csv_writer.writerows(data)
```

Example of writing as `dict`:

```python
import csv

data = [{'Name': 'Daniel', 'Age': 24, 'City': 'Madrid'},
        {'Name': 'Álex', 'Age': 23, 'City': 'Gijón'}]

with open('output.csv', 'w', newline='') as file:
    fieldnames = ['Name', 'Age', 'City']
    csv_writer = csv.DictWriter(file, fieldnames=fieldnames)
    csv_writer.writeheader()
    csv_writer.writerows(data)
```

## Using pandas for CSV

`pandas` provides powerful functionality for reading, writing, and manipulating CSV data.

It is highly recommended for handling large datasets efficiently.

Must be installed with `pip`.

Example of writing with `pandas`:

```python
import pandas as pd

data = {'Name': ['Daniel', 'Álex'], 'Age': [24, 23], 'City': ['Madrid', 'Gijón']}
df = pd.DataFrame(data)

df.to_csv('example.csv', index=False)
```

Example of reading with `pandas`:

```python
import pandas as pd

df = pd.read_csv('example.csv')
print(df)
```

Output:

```Plain Text
#     Name  Age       City
0   Daniel   24     Madrid
1     Álex   23      Gijón
```