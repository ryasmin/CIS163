# Custom (User-Defined) Exceptions

Python allows you to create your own exceptions by defining a new class that inherits from the built-in `Exception` class (or another built-in exception such as `ValueError`).

---

### Why use custom exceptions?
- To make error messages more meaningful.
- To distinguish between different types of errors.
- To improve readability and maintainability of your code.

---

### Exercise 1: With Built-in Exception

```
try:
    l = float(input())
    w = float(input())
    if l < 0 or w < 0:
      raise ValueError("Inputs cannot be negative.")

    print(f"Area: {l * w}")

except ValueError as msg:
    print(msg)
```

Questions:
- What happens if you enter 5 and 3?
- What happens if you enter -2 and 4?
- What happens if you enter "abc" for one of the inputs?

> Think: In which cases is the ValueError raised by you, and in which cases is it raised automatically by Python?

---
### Exercise 2: Replacing with Custom Exception

```
class NegativeError(Exception):
    pass

try:
    l = float(input())
    w = float(input())
    if l < 0 or w < 0:
      raise NegativeError("Inputs cannot be negative.")

    print(f"Area: {l * w}")

except NegativeError as msg:
    print(msg)
```
Questions:
- How is this behavior similar to Exercise 1?
- What advantage do you get by using a named custom exception (`NegativeError`) instead of `ValueError`?
- What happens if the user enters `"abc"` again? Which exception is raised now, and is it caught?

> ___Note___: A custom exception class must inherit from `Exception` (or another built-in exception), e.g. `class MyError(Exception):`.

---

### Exercise 3: Custom Exception with `__str__`

```
class NegativeError(Exception):
    def __init__(self):
        pass
    def __str__(self):
        return f"Inputs cannot be negative."

try:
    l = float(input())
    w = float(input())
    if l < 0 or w < 0:
      raise NegativeError

    print(f"Area: {l * w}")

except NegativeError as msg:
    print(msg)
```
> ___Advantage___: If the same error message is used repeatedly, this approach avoids duplication and keeps the code cleaner.

---

### Exercise 4: Custom Exception with Additional Information

```
class NegativeError(Exception):
    def __init__(self, value, dimension_name):
        self.value = value
        self.dimension_name = dimension_name
    def __str__(self):
        return f"{dimension_name} cannot be negative: {value}"

try:
    l = float(input())
    w = float(input())
    if l < 0:
      raise NegativeError(l, "Length")
    if w < 0:
      raise NegativeError(w, "Width")

    print(f"Area: {l * w}")

except NegativeError as msg:
    print(msg)
```
> ___Notice___: The error message now tells you which input was wrong and what its value was.

