# Overview of OOP Principle
The Four Pillars of OOP
1. Encapsulation: 
    - Protect and Control access to internal data
    - Avoid accidental modifications
2. Abstraction: 
    - Hiding Unnecessary implementation details
    - Creating Consistent and structured framework
3. Inheritance
    - Reusability and extension of another class
4. Polymorphism
    - Interchangeable code
    - Create flexible and scalable design

<br>

---

# Polymorphism Basics
> Poly - > many, Morph -> form

__Definition:__ Use the same method (function) name on (with) different objects (parameters) and depending on the object (parameters), it will do different things

## Four different ways to achieve Polymorphism in Python
### 1. Duck Typing
  ```
  Dog: speak() -> “woof”
  Cat: speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Dog())
  myfunc(Cat())
  ```
### 2. Interface
  ```
  Animal:      speak(): @abtractmethod 
  Dog(Animal): speak() -> “woof”
  Cat(Animal): speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Dog())
  myfunc(Cat())
  ```

### 3. Inheritance/ Method Overriding
  ```
  Animal:      speak() -> “generic sound”
  Dog(Animal): speak() -> “woof”
  Cat(Animal): speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Animal())
  myfunc(Dog())
  myfunc(Cat())
  ```

<br>

---
---
#### Why Polymorphism is important:
1. Otherwise creates long chain of conditionals
    ```
  	if isinstance(obj, Dog):
  		obj.dog_speak()
  	if isinstance(obj, Cat):
  		obj.cat_speak()
    ...
    ```
2. Maintenance issue
    - If another class say `Pig` needs to be added, you will need to go in and change the if-else conditions.
    - Easily breaks code if not careful.
  
#### Method Signature
A method signature describes:
1. The method name
2. The parameters

> For polymorphism to work properly, method signatures must be compatible.
```
RobotDog: speak(volume) -> “beep at {volume}”
```

- __Problem:__ If we pass `RobotDog` to `myfunc` we get a `TypeError`.

- __Why?__ Because the method signatures are different, even though both classes have a method named speak, they are not polymorphically compatible.

- __Solution:__ Make every `speak` method accept the same parameters.
  ```
  Dog:      speak(volume=None) -> “woof”
  Cat:      speak(volume=None) -> “meow”
  RobotDog: speak(volume)      -> “beep at {volume}”
  ```

- __Takeaway:__ Polymorphism is not just “same method name.” It is:
  - Same method name
  - Compatible method signature (parameters + types)

---
---

<br>

### 4. Operator Overloading

What Happens When We Use Operators?
- `5 + 3 = 8`              -> Integer Addition
- `"hi" + "bye" = "hibye"` -> String Concatenation
- `[1] + [2] = [1, 2]`     -> List Concatenation

The `+` operator behaves differently depending on the object type - Polymorphism.

What is Actually Happening?
```
a = 5
b = 3
c = a + b
c = a.__add__(b)
```
> In Python, operators are syntactic sugar for special/dunder/magic methods (double underscore).

Similarly:
- `a - b → a.__sub__(b)`
- `a * b → a.__mul__(b)`
- `a == b → a.__eq__(b)`
- `len(a) → a.__len__()`

---

___Example 1:___
```
class MyInt:
  def __init__(self, value):
    self.value = value

  def __add__(self, other):
    return self.value + other.value

a = MyInt(5)
b = MyInt(3)
c = a.__add__(b)
```

Explanation:
```
a → self      self.value  → a.value → 5
b → other     other.value → b.value → 3
```

---

___Example 2:___
```
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return (self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return (self.x - other.x, self.y - other.y)

v1 = Vector(2, 3)
v2 = Vector(1, 4)

print(v1 + v2)          # Output: (3, 7)
print(v1.__add__(v2))   # Output: (3, 7)

print(v1 - v2)          # Output: (1, -1)
print(v1.__sub__(v2))   # Output: (1, -1)
```

Explanation:
```
v1 → self      self.x  → v1.x → 2      self.y  → v1.y → 3
v2 → other     other.x → v2.x → 1      other.y → v2.y → 4
```

<br>

Variation 1: Return a new `Vector` object instead of a `tuple`
```
class Vector:
    ...
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    def __str__(self):
        return f"({self.x}, {self.y})"

print(v1 + v2)          # Output: (3, 7)
print(v1.__add__(v2))   # Output: (3, 7)
```
Note: Does not print properly without `__str__`.

<br>

Variation 2: Vector Multiplication
```
class Vector:
    ...
    def __mul__(self, other):
        return (self.x * other.x) + (self.y * other.y)

v1 = Vector(2, 3)
v2 = Vector(1, 4)

print(v1 * v2)          # Output: 14
print(v1.__mul__(v2))   # Output: 14
```

<br>

Variation 3: Scalar Multiplication
```
class Vector:
    ...
    def __mul__(self, other):
        return (self.x * other, self.y * other)

v1 = Vector(2, 3)

print(v1 * 2)          # Output: (4, 6)
print(v1.__mul__(2))   # Output: (4, 6)
```

<br>

Variation 4: Scalar Multiplication in opposite Order
```
class Vector:
    ...
    def __mul__(self, other):
        return (self.x * other, self.y * other)

    def __rmul__(self, other):
        return self.__mul__(other)

v1 = Vector(2, 3)

print(2 * v1)          # Output: (4, 6)
```

- Python tries: `left.__mul__(right)`
- If that fails tries: `right.__rmul__(left)`

<br>

Variation 5: Both Vector and Scalar Multiplication
```
class Vector:
    ...
    def __mul__(self, other):
        if isinstance(other, (int, float)):
          return (self.x * other, self.y * other)
        if isinstance(other, Vector):
          return (self.x * other.x) + (self.y * other.y)

v1 = Vector(2, 3)
v2 = Vector(1, 4)

print(v1 * v2)          # Output: 14
print(v1 * 2)           # Output: (4, 6)
```
