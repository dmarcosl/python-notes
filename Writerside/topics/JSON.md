# JSON

## Reading and writing JSON files

The `json` module allows reading and writing JSON files using `json.load()` and `json.dump()`.

JSON objects are mapped to `dict`, while JSON arrays are converted into `list`. Other native types, such as strings, integers, floats, and booleans, are also directly supported.

Example writing a `dict` to a JSON file:

```python
import json

data = {'name': 'Daniel', 'age': 24}
with open('data.json', 'w') as file:
    json.dump(data, file)
```

Example reading a JSON file into a `dict`:

```python
with open('data.json', 'r') as file:
    loaded_data = json.load(file)
print(loaded_data)
```

Output:

```python
{'name': 'Daniel', 'age': 24}
```

## Parsing JSON data

To parse a JSON `string` into a Python object, use `json.loads()`.

Example:

```python
json_string = '{"name": "Daniel", "age": 24}'
parsed_data = json.loads(json_string)
print(parsed_data['name'])
```

Output:

```Plain Text
Daniel
```

## Handling complex data structures in JSON

For custom objects, define a function for serialization.

Example:

```python
class City:
    def __init__(self, name, temperature):
        self.name = name
        self.temperature = temperature

def city_to_dict(city):
    return {'name': city.name, 'temperature': city.temperature}

city = City('Madrid', 45)
json_data = json.dumps(city, default=city_to_dict)
print(json_data)
```

Output:

```python
{'name': 'Madrid', 'temperature': 45}
```