# Conditionals

## if, elif, and else Statements

Python provides `if`, `elif` and `else` statements to evaluate conditions.

```python
if n1 > n2:
    print('n1 is higher than n2')
elif n1 < n2:
    print('n1 is lesser than n2')
else:
    print('n1 is equals to n2')
```

Several conditions can be used in the same `if` statement by using `and` and `or` operators.

```python
if (n1 > 5 and n2 > 6) or n1 < 1:
    print('n1 is higher than 5 and n2 is higher than 6')
    print('or n1 is lesser than 1')
```

Others operators can be used in the conditions.

```python
if n1 in [1, 2, 3, 4]:
    print('n1 is contained in the list')
elif n1 is False:
    print('n1 is False')
elif type(n1) is int:
    print('the type of n1 is int')
```

Some conditions can be combined.

```python
if n1 > n2 < n3:
    print('n1 is higher than n2 and n2 is lesser than n3)
elif n1 > n2 and n2 < n3:
    print('the same as before')
```

## Ternary Operator

The ternary operator allows you to write simple `if`-`else` conditions in a single line.

Syntax:

```python
result = value_if_true if condition else value_if_false
```
Example:

```python
age = 16
message = 'You can drink.' if age >= 18 else 'You can't drink.'
print(message)
```

Output:

```Plain Text
You can't drink.
```