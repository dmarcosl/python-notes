# Classes and Objects

## Class Definition

A class is a blueprint for creating objects (instances).

It defines the attributes and behaviors that the objects created from it will have.

Example of an empty class, just defining the structure:

```python
class Person:
    pass
```

## Constructor

The constructor method `__init__` is a special method in Python classes.

It is automatically called when a new object (instance) of the class is created.

This method is used to initialize the attributes of the object.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

## Instance vs. Class Variables

A class can have instance variables (specific to each object) and class variables (shared by all objects of the class).

Each instance of a class can have its own set of attributes, but class variables are shared among all instances.


```python
class Person:
    city = 'Madrid'  # Class variable shared by all instances
    def __init__(self, name, age):
        self.name = name  # Instance variable unique to each instance
        self.age = age  # Instance variable unique to each instance
```

## Object Creation

Once a class is defined, you can create an object (or instance) of that class.

To create an object, call the class name and pass the arguments required by the constructor.

```python
person1 = Person('Daniel', 24)
person2 = Person('Álex', 23)
```

## Methods

A method is a function defined inside a class that operates on instances of that class.

Methods must always include self as the first parameter, which represents the instance of the class.

```python
class Person:
    city = 'Madrid'
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        print(f'Hello, my name is {self.name}, I am {self.age} and I live in {Person.city}.')
```

Calling the method:

```python
person1 = Person('Daniel', 30)
person1.greet()
```

Output:

```Plain Text
Hello, my name is Daniel, I am 30 and I live in Madrid.
```

## Inheritance

Inheritance allows one class (the child class) to inherit the attributes and methods from another class (the parent class).

This is useful when you want to create a new class that has the same behavior as an existing class, with additional or modified behavior.

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print(f'{self.name} says woof!')
```

Calling the method:

```python
animal = Animal('Animalus')
animal.speak()
dog = Dog('doge')
dog.speak()
```

Output:

```Plain Text
doge says woof!
```

## Class Methods and Static Methods

Class Method is a method that is bound to the class, not the instance. It is often used to modify the state of the class.

Static Method is a method that doesn't access or modify the class state or instance state. It's a general utility function that could be placed within the class for organizational purposes.

Example:

```python
class Car:
    wheels = 4

    def __init__(self, make, model):
        self.make = make
        self.model = model

    @classmethod
    def change_wheels(cls, new_wheels):
        cls.wheels = new_wheels
    
    @classmethod
    def display_info(cls):
        print(f'Cars have {cls.wheels} wheels.')
```

Calling the methods:

```python
car1 = Car('Toyota', 'Corolla')
car2 = Car('Honda', 'Civic')

Car.change_wheels(6)

car1.display_info() 
car2.display_info()
```

Output:

```Plain Text
Cars have 6 wheels.
Cars have 6 wheels.
```

## Magic Methods

Python supports special methods that are commonly known as "magic" or "dunder" methods because they are surrounded by double underscores `__`.

These methods allow you to define custom behavior for operations like object creation, string representation, and arithmetic operations.

Example:

```python
class Dog:
    def __init__(self, name, toys):
        self.name = name
        self.toys = toys
    
    def __str__(self):
        return f'A dog named {self.name} with {self.toys} toys'
        
    def __add__(self, more_toys):
        return self.toys += more_toys
```
