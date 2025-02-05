# Functions

## Defining Functions

A function is a block of reusable code that performs a specific task.

In Python, you define a function using the `def` keyword, followed by the function name and parentheses enclosing any parameters.

The function body is indented.

Syntax:

```python
def function_name(parameters):
    # Block of code
```

Example:

```python
def greet(name):
    print('Hello, ' + name + '!')
```

Calling the Function:

```python
greet('Alice')  # Output: Hello, Alice!
greet('Bob')    # Output: Hello, Bob!
```

## Return Statement

The `return` statement is used to send a result back from the function to the caller.

After the `return` statement is executed, the function exits and the control is returned to the place where the function was called.

Syntax:

```python
def function_name(parameters):
    # Block of code
    return value
```

Example:

```python
def add(a, b):
    result = a + b
    return result
```

Calling the Function:

```python
sum = add(3, 4)
print(sum)  # Output: 7
```

## Lambda Functions

A `lambda` function is a small, anonymous function defined using the `lambda` keyword.

It can take any number of arguments but can only have one expression.

The expression is evaluated and returned when the `lambda` function is called.

Syntax:

```python
lambda parameters: expression
```

Example:

```python
multiply = lambda x, y: x * y
```

Calling the `lambda`:

```python
result = multiply(3, 4)
print(result)  # Output: 12
```

## Default Arguments

You can assign default values to parameters when defining a function.

These default values will be used if no argument is passed for those parameters when the function is called.

Example:

```python
def greet(name='Guest'):
    print('Hello, ' + name + '!')
```

Calling the Function:

```python
greet()         # Output: Hello, Guest!
greet('Alice')  # Output: Hello, Alice!
```

## Keyword Arguments

You can also specify the values of arguments by their parameter names when calling a function.

Example:

```python
def introduce(name, age):
    print('My name is ' + name + ' and I am ' + str(age) + '.')
```

Calling the Function:

```python
introduce(age=24, name='Daniel')
```

Output:

```Plain Text
My name is Daniel and I am 24.
```

## Arbitrary Arguments

`*args` allows you to pass a variable number of non-keyword arguments (positional arguments) to a function.

`**kwargs` allows you to pass a variable number of keyword arguments to a function.

Example:

```python
def my_function(name, *args, age=None, **kwargs):
    print(name)
    print(args)
    print(age)
    print(kwargs)
```

Calling the Function:

```python
my_function('Daniel', 1, 2, 3, 4, height=182)
```

Output:
```Plain Text
Daniel
(1, 2, 3, 4)
None
{'height': 182}
```

## Docstrings

A docstring is a special type of string that is used to document a function.

It is placed immediately after the function definition and can be accessed using the `help()` function or `.__doc__.`

Example:

```python
def greet(name):
    """This function greets the person passed in as a parameter."""
    print('Hello, ' + name + '!')
```

Calling the Function:

``` python
print(greet.__doc__)
```

Output:

```Plain Text
This function greets the person passed in as a parameter.
```

## Returning Multiple Values

A function in Python can return multiple values.

These values are returned as a `tuple`, which is implicitly created when multiple values are returned. You can then unpack these values into separate variables when calling the function.

Example: 

```python
def get_coordinates():
    return 4, 5, 'Madrid'
```

Calling the Function:

```python
x, y, city = get_coordinates()
print(x, y, city)
```

Output:

```python
4 5 Madrid
```
