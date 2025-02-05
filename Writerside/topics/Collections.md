# Collections

## List

Lists can be created using `list()` or `[]`.

```python
cities = list('Madrid', 'Tokyo')
cities = ['Madrid', 'Tokyo']
```

Some common operations:

```python
numbers = [1, 2, 3]
numbers[0]          # Access by index
numbers.append(4)   # Add an element
numbers.remove(2)   # Remove an element
numbers.sort()      # Sort the list
numbers.reverse()   # Reverse the list
numbers[1:3]        # Slice the list
```

## Tuple

Tuples can be created using `tuple()`, `()` or several values separated by comma.

```python
numbers = tuple([1, 2, 3])
numbers = (1, 2, 3)
numbers = 1, 2, 3
```

You can access elements by index or slice them, but tuples are immutable, so their values can't be changed.

```python
coordinates = (10, 20)
coordinates[0]         # Access by index
coordinates[1:]        # Slice the tuple
```

## Set

Sets can be created with `set()` or `{}`.

```python
fruit = set(['apple', 'banana', 'pineapple'])
fruit = {'apple', 'banana', 'pineapple'}
```

Some common operations:

```python
unique_numbers = {1, 2, 3}
unique_numbers.add(4)      # Add an element
unique_numbers.remove(1)   # Remove an element

set1 = {1, 2}
set2 = {2, 3}
set1 | set2                # Union
set1 & set2                # Intersection
set1 - set2                # Difference
```

| Operation                   | Equivalent | Result                                                  |
|-----------------------------|------------|---------------------------------------------------------|
| `a.issubset(b)`             | `a <= b`   | Checks if `a` is inside `b`                             |
| `a.issuperset(b)`           | `a >= b`   | Checks if `b` is inside `a`                             |
| `a.union(b)`                | `a \| b`   | New set with the elements of both                       |
| `a.intersection(b)`         | `a & b`    | New set with the elements common to both                |
| `a.difference(b)`           | `a - b`    | New set with elements in `a` but not in `b`             |
| `a.symmetric_difference(b)` | `a ^ b`    | New set with elements in either `a` or `b` but not both |

## Dictionary

Dictionaries are created with `dict()` or `{key: value}`.

```python
score = dict('dani' : 6, 'fanta' : 5)
score = {'dani' : 6, 'fanta' : 5}
```

Dictionaries are the same as a JSON in JS or a Map in Java.

Some common operations:

```python
person = {'name': 'Daniel', 'age': 24}
person['name']              # Access value by key
person.get('name')          # Access value by key safely
person.get('name', 'None')  # Access value by key safely, default if missing
person['age'] = 26          # Update value
del person['name']          # Delete a key-value pair
person.keys()               # Get all keys
person.values()             # Get all values
person.items()              # Get all pairs of keys values
```