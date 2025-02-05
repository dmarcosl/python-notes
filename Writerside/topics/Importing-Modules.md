# Importing Modules

## Standard Library

The Standard Library is a collection of modules that come pre-installed with Python.

### Importing a whole module

You can import an entire module to access its functions, classes, and variables.

Example:

```python
import math
print(math.sqrt(16))  # Outputs: 4.0
```

### Importing specific functions or classes from a module

This allows you to import only the functions or classes you need, making your code cleaner and more efficient.

```python
from math import sqrt
print(sqrt(16))  # Outputs: 4.0
```

## Third-party Libraries

Third-party libraries are additional modules that are not included in the Python standard library but can be installed via `pip`.

### Importing a third-party library

```python
import requests
response = requests.get('https://api.example.com')
print(response.status_code)
```

## Aliases

You can assign an alias to a module or function to simplify its usage, especially if the names are long.

### Using an alias for a module

```python
import numpy as np
arr = np.array([1, 2, 3])
print(arr)
```

### Using an alias for a function

```python
from math import sqrt as square_root
print(square_root(16))
```