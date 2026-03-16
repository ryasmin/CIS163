# Abstraction in Python
Abstraction means focusing on what an object should do instead of how it does it.

In Python, abstraction is commonly implemented using:
- `ABC` -> Abstract Base Class
- `@abstractmethod` -> marks methods that subclasses must implement

Abstraction helps us create a blueprint for other classes.

<br>

## Step 1 — Lets's Start With the Problem

Suppose we have different shapes. Each shape should be able to:
- calculate area
- calculate perimeter

Here is one way to write that:
```python
import math

class Circle:
    def __init__(self, radius: float):
        self.radius = radius

    def area(self) -> float:
        return math.pi * self.radius ** 2

    def perimeter(self) -> float:
        return 2 * math.pi * self.radius


class Rectangle:
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height

    def area(self) -> float:
        return self.width * self.height

    def perimeter(self) -> float:
        return 2 * (self.width + self.height)


def describe(shape):
    return f"Area = {shape.area():.2f}, Perimeter = {shape.perimeter():.2f}"


shapes = [Circle(3), Rectangle(4, 5)]

for s in shapes:
    print(describe(s))
```

<br>

## Step 2 — Now What Is the Problem Exactly?

The problem is that Python is only trusting us. There is NO rule forcing every shape class to implement both methods.

For example:
```python
class Triangle:
    def __init__(self, base, height):
        self.base = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height

t = Triangle(4, 6)
print(describe(t))
```

we get an error at runtime because `Triangle` has no `perimeter()` method.

That is what abstraction helps prevent.

<br>

## Step 3 — Abstract Base Class (ABC)

Python provides a module called `abc`.

We import:
```python
from abc import ABC, abstractmethod
```
Here:
- `ABC` lets us define an abstract base class
- `@abstractmethod` marks methods that subclasses must implement

Now let us create a blueprint for all shapes.
```python
from abc import ABC, abstractmethod
import math

class Shape(ABC):

    @abstractmethod
    def area(self) -> float:
        pass

    @abstractmethod
    def perimeter(self) -> float:
        pass
```

This class says:
  > Any subclass of Shape must define area() and perimeter().

---

#### Important Rule to Remember
You cannot create an object from an abstract class directly.

This will fail:
```python
s = Shape()
```

__Why?__
- Because Shape is incomplete (i.e., has an abstract method).
---

<br>

## Step 4 — Create Concrete Subclasses

A concrete class is a normal class that fully implements all required abstract methods.

```python
class Circle(Shape):
  # Rest of the code from before
  ...

class Rectangle(Shape):
  # Rest of the code from before
  ...
```

<br>

## Step 5 — Abstract Method vs Concrete Method

An abstract class can contain:
- abstract methods -> must be implemented by subclasses
- concrete methods -> already implemented in the parent and shared by subclasses

```python
class Shape(ABC):

    @abstractmethod
    def area(self) -> float:
        pass

    @abstractmethod
    def perimeter(self) -> float:
        pass

    def summary(self) -> str:
        return f"Area = {self.area():.2f}, Perimeter = {self.perimeter():.2f}"
```

Here:
- `area()` is abstract
- `perimeter()` is abstract
- `summary()` is concrete

So every subclass must define `area()` and `perimeter()`, but they automatically inherit `summary()`.

```python
class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side

    def perimeter(self):
        return 4 * self.side


sq = Square(5)
print(sq.summary())        # Output: Area = 25.00, Perimeter = 20.00
```

<br>

## Interface-Like Behavior

Python has no interface keyword. It uses abstract class with only abstract methods.
```python
class Flyable(ABC):
    @abstractmethod
    def fly(self):
        pass

class Bird(Flyable):
    def fly(self):
        return "Bird flying"


class Airplane(Flyable):
    def fly(self):
        return "Plane flying"
```



<br>

## Key Vocabulary

| Term | Description |
|------|------------|
| Abstract Method | A method declared with `@abstractmethod`. <br> Subclasses must implement it. |
| Concrete Method | A normal method with a body, already implemented. |
| Abstract Class | A class that cannot be instantiated directly. <br> It acts as a blueprint for subclasses. <br> Can have `__init__` method. <br> Can have concrete methods.|
| Concrete Class | A subclass that implements all required abstract methods. |
| Interface-Like Behavior | Using an abstract class with only abstract methods to enforce a contract. <br> Cannot have `__init__` method. <br> Cannot have concrete method.|
