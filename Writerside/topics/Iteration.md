# Iteration

## For Loop

The `for` loop allows iteration over elements in a collection (such as lists, strings, or ranges).

### Iterating Over a List

Example:

```python
colors = ['Red', 'Black', 'White']
for color in colors:
    print(f'Is {color} your favorite?')
```

Output:

```plain text
Is Red your favorite?
Is Black your favorite?
Is White your favorite?
```

### Iterating Over Numbers and Calculations

Example:

```python
for number in [1, 2, 3, 4]:
    double = number * 2
    print(f'Twice {number} is {double}')
```

Output:

```Plain Text
Twice 1 is 2
Twice 2 is 4
Twice 3 is 6
Twice 4 is 8
```

### Iterating Over Characters of a String

Example:

```python
for character in 'hello':
    print(character)
```

Output:

```Plain Text
h
e
l
l
o
```

### Iterating Over a Range of Numbers

Example:

```python
for i in range(0, 50, 5):
    print(i, end=' ')
```

Output:

```Plain Text
0 5 10 15 20 25 30 35 40 45
```

### Skipping Items in a List

You can use slicing to iterate over every other item in the list

Example:

```python
colors = ['Red', 'Black', 'Yellow', 'Green', 'Blue', 'Purple']
for color in colors[::2]:
    print(color, end=' ')
```

Output:

```Plain Text
Red Yellow Blue
```

## While Loop

The `while` loop repeats a block of code as long as a given condition is `True`.

Example:

```python
countdown = 10
while countdown >= 0:
    print(countdown, end=' ')
    countdown -= 1
```

Output:

```Plain Text
10 9 8 7 6 5 4 3 2 1 0
```

## Iterators

An iterator allows you to traverse through a collection, such as a `list`, `tuple`, `set`, or `string`.

Once an iterator has exhausted its values, it will raise an error if you attempt to retrieve another element.

Example:

```python
colors = ['Red', 'Black', 'Yellow', 'Green', 'Blue', 'Purple']
iter_color = iter(colors)
print(next(iter_color))
print(next(iter_color))
```

Output:

```Plain Text
Red
Black
```

Behind the scenes, a for loop implicitly calls `iter()` and `next()` to iterate over the elements.

## Range

`range()` generates an immutable sequence of numbers and is commonly used for looping a specific number of times in a for loop.

Syntax:

```python
range(start, stop, step)
```

- start: Starting value (inclusive)
- stop: Ending value (exclusive)
- step: Increment (default is 1)

Example: 

```python
list(range(0, 10, 2))
```

Output:

```Plain Text
[0, 2, 4, 6, 8]
```

The `range` object only stores the values for start, stop, and step, and **does not hold all the numbers in memory**.

### Using range with For Loop

Example:

```python
for i in range(0, 10, 2):
    print(i, end=' ')
```

Output:

```Plain Text
0 2 4 6 8
```

### Range Slicing and Negative Indices

You can perform slicing and index lookups on range objects.

Example:

```python
# Containment test
print(11 in range(0, 20, 2))  # False
print(10 in range(0, 20, 2))  # True

# Index lookup
print(range(0, 20, 2).index(10))  # 5

# Accessing elements by index
print(range(0, 20, 2)[5])  # 10

# Accessing elements by negative index
print(range(0, 20, 2)[-1])  # 18
```

Output:

```Plain Text
False
True
5
10
18
```

### Reversing a Range

Example:

```python
for i in range(0, 10)[::-1]:
    print(i, end=', ')
```

Output:

```Plain Text
9, 8, 7, 6, 5, 4, 3, 2, 1, 0,
```

## continue in Loops

The `continue` statement skips the current iteration and continues with the next iteration of the loop.

Example:

```python
for i in range(5):
    if i == 3:
        continue
    print(i, end=' ')
```

Output:

```Plain Text
0 1 2 4
```

## break in Loops

The `break` statement exits the loop.

Example:

```python
for i in range(5):
    if i == 2:
        print('Breaking the loop')
        break
    print(i)
```

Output:

```Plain Text
0
1
Breaking the loop
```

## else in Loops

An `else` block can be used with `for` and `while` loops. It will run if the loop completes normally, without hitting a break statement.

Example with `for`:

```python
for number in range(5):
    print(number, end=' ')
else:
    print('Loop completed without interruption.')
```

Output:

```Plain Text
0 1 2 3 4 Loop completed without interruption.
```

Example with `while`:

```python
countdown = 5
while countdown > 0:
    print(countdown)
    countdown -= 1
else:
    print('Countdown finished!')
```

Output:

```Plain Text
5
4
3
2
1
Countdown finished!
```

Example with `break`:

```python
for number in range(5):
    if number == 3:
        break
    print(number)
else:
    print('Loop completed without interruption.')
```

```python
0
1
2
```

## Enumerating over a collection with enumerate

The `enumerate()` function is useful when you need both the index and the value in a loop.

Example:

```python
colors = ['Red', 'Black', 'Yellow', 'Green']
for index, color in enumerate(colors):
    print(f'{index}: {color}')
```

Output:

```Plain Text
0: Red
1: Black
2: Yellow
3: Green
```

## Using zip() to iterate over multiple collections

The `zip()` function allows to iterate over several collections at the same time.

Example:

```python
names = ['Alice', 'Bob', 'Charlie']
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f'{name}: {score}')
```

Output:

```Plain Text
Alice: 85
Bob: 92
Charlie: 78
```