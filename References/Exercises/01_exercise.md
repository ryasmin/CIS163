### Exercise 1 — Immutable Reassignment
> Immutables cannot be modified in-place. Assignment inside a function creates a new binding.
```python
def square(n):
     n *= n

arg = 4
square(arg)
print(arg)
```

### Exercise 2 — Local vs Global
```python
def greet(name, counter):
     counter += 1
     return f"Hi, {name}!"

counter = 0
print(greet("Alice", counter))
print(f"Counter is {counter}")
print(greet("Bob", counter))
print(f"Counter is {counter}")
```

### Exercise 3 — List Aliasing
> Multiple variables can reference the same object.
```python
a = [1, 2, 3]
b = a
b.append(99)

print(a)
print(b)
```

### Exercise 4 — Dictionary Mutation
> Mutating a mutable object inside a function affects the caller.
```python
def square(num_dict):
     num_dict["n"] *= num_dict["n"]

mt = {"n": 4}
square(mt)
print(mt)
```

What if I change it to:
```python
def square(num_dict):
     num_dict["n"] *= num_dict["n"]
     num_dict["m"] = 17

mt = {"n": 4}
square(mt)
print(mt)
```

### Exercise 5 — Default Immutable
```python
def modify_string(s2, s1 = "Hello"):
    s1 += " " + s2
    return s1

a = modify_string("World")
b = modify_string("Class")

print(a)
print(b)
```

### Exercise 6 — Default Mutable in Function
> Default arguments are created once.
```python
def add_item(item, container=[]):
    container.append(item)
    return container

list1 = add_item(1)
list2 = add_item(2)

print(list1)
print(list2)
```

### Exercise 7 — Default Mutable in Class Constructor
> The same default list can be shared across instances.
```python
class Example:
    def __init__(self, name, items=[]):  # Mutable default!
        self.name = name
        self.items = items

    def add_item(self, item):
        self.items.append(item)

a = Example("A")
b = Example("B")

a.add_item("apple")
b.add_item("banana")

print(a.items)
print(b.items)
```

### Exercise 8 — Object Aliasing
> Reassigning a variable does not clone an object.
```python
class Balloon:
    def __init__(self, color):
        self.color = color

b1 = Balloon("orange")
b2 = Balloon("orange")

b3 = b2
b2.color = "black"

print(b1.color)
print(b2.color)
print(b3.color)
```

### Exercise 9 — Reassignment Inside Function
> Reassigning a parameter does not affect the caller.
```python
def mystery(first, second):
    first = second

b1 = Balloon("red")
b2 = Balloon("blue")

mystery(b1, b2)

print(b1.color)
```

### Exercise 10 — Mutation Inside Function
> Mutating an object through a parameter does affect the caller.
```python
def repaint(balloon):
    balloon.color = "green"

b = Balloon("yellow")
repaint(b)

print(b.color)
```

### Exercise 11 — Returning Existing Object
> Returning an object reference shares the same object.
```python
def change_color(b):
    b.color = "blue"
    return b

b1 = Balloon("white")
b2 = change_color(b1)

b2.color = "pink"

print(b1.color)
print(b2.color)
```

### Exercise 12 — Hidden Mutation via `__add__`
> Operator overloading can mutate unexpectedly. Be careful of the return value.
```python
class Box:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        self.value += other.value 
        return self

b1 = Box(10)
b2 = Box(20)

b3 = b1 + b2  

print(b3.value)
print(b1.value)
```

What if I change it to:

```python
class Box:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        self.value += other.value 
        return Box(self.value)      # ----- Changes made------

b1 = Box(10)
b2 = Box(20)

b3 = b1 + b2  

print(b3.value)
print(b1.value)
```

What if I change it to:

```python
class Box:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        value = self.value + other.value 
        return Box(value)      # ----- Changes made------

b1 = Box(10)
b2 = Box(20)

b3 = b1 + b2  

print(b3.value)
print(b1.value)
```
