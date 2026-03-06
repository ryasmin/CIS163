## Part 1 — Instance Methods (Baseline)
Every method you’ve written so far probably looked like this:
```python
class Calculator:

    def __init__(self, name, version):
        self.name = name
        self.version = version

    def get_calculator_info(self):
        return f"{self.name} V.{self.version}"
```
> <mark>These are called "Instance Methods"</mark>

- Takes `self`
- Operate on object data (attributes)
- Require an instance to call
  
```python
calc = Calculator("MyCalculator", 1)
print(calc.get_calculator_info())
```

<br>

### When a Method Does NOT Need `self`
Now consider the following method:
```python
class Calculator:
  ...
  def add_numbers(self, nums):
      return sum(nums)
```
- It does not use `self`.
- It does not use any instance data such as: `name` or `version`.

This is where `@staticmethod` becomes useful.

<br>

## Part 2 — `@staticmethod`
A __Static__ method:
- Does NOT take `self` or `cls`
- Does NOT access instance or class attributes
- Is logically related to the class

1. Convert to Static Method
```python
class Calculator:
    ...
    @staticmethod
    def add_numbers(nums):
        return sum(nums)
```

2. How to call it
```python
Calculator.add_numbers([1, 2, 3, 4])
```
   - DO NOT need an instance to call.

#### Example: Calender Validation

```python
import datetime

class Calendar:

    def __init__(self):
        self.events = {}

    def add_event(self, name, date):
        if not Calendar.is_weekend(date):
            self.events[name] = date
            print("Event added.")
        else:
            print("Event falls on a weekend.")

    @staticmethod
    def is_weekend(date):
        return date.weekday() > 4

exam = datetime.date(2025, 2, 20)
print(Calendar.is_weekend(exam))
```

<br>

### When You Need Access to the Class 
Sometimes you don’t need instance data. But you DO need class data.
- class variables
- class name

That’s where `@classmethod` comes in.

<br>

## Part 3 — `@classmethod`
A __Class__ method:
- Takes `cls` as the first parameter
- Operates on the class itself

Use cases:
- To modify class attributes
- Often used as alternative constructors

<br>

### Use Case 1 — As Alternative Constructor
```python
class Employee:
    # Class Attributes
    raise_amt = 1.04

    def __init__(self, name, pay):
        # Instance Attributes
        self.name = name
        self.pay = int(pay)

    @classmethod
    def from_string(cls, emp_str):
        name, pay = emp_str.split('-')
        return cls(name, pay)

emp = Employee.from_string("John-50000")
```

<br>

#### Why NOT use an Instance Method?

```python
class Employee:
    ...
    def from_string(self, emp_str):
        name, pay = emp_str.split('-')
        return Employee(name, pay)
        
dummy = Employee("dummy", 0)
emp = dummy.from_string("John-50000")  # Awkward
```
- Cannot call without creating an instance
- Needs to use class name
- Issues
      - if class name changes - need to manually change everywhere you have `Employee`
      - if inheritance comes into play cannot create child instance

Example for Inheritance
```python
class Employee:
    ...
    def from_string(self, emp_str):
        name, pay = emp_str.split('-')
        return Employee(name, pay)

class SalaryEmployee(Employee):
    pass

dummy = SalaryEmployee("dummy", 0)
emp = dummy.from_string("John-50000")
print(type(emp)))                # Employee
```

Here `emp` is an instance of the `Employee` class, NOT `SalaryEmployee`.

<br>

#### Why NOT use a Static Method?
```python
class Employee:
    ...
    @staticmethod
    def from_string(emp_str):
        name, pay = emp_str.split('-')
        return Employee(name, pay)        # Hard-coded
        
emp = Employee.from_string("John-50000")  
```
- Needs to use class name (issue if name changed or inherited)

<br>

### Use Case 2 — For Modifying Class-Level Data
In the example of Use Case 1, `raise_amt ` was a class variable.
If you want to change it, you can using 
```python
Employee.raise_amt = 150000
```

What if you want to provide validation for setting a new value for it? Use `classmethod`.
```python
class Employee:
    raise_amt = 1.04
    ...
    @classmethod
    def set_raise_amt(cls, amt):
        if not isinstance(amt, float):
            raise TypeError
        if amt < 0 or amt > 2:
            raise ValueError
        cls.raise_amt = amt

Employee.set_raise_amt(2.0)
```

<br>

## Decision Framework 

When writing a method, ask:

1️⃣ Does it use instance data? → Yes → Instance method (`self`)

2️⃣ Does it use class-level data (or name) but not instance data? → Yes → Class method (`cls`)

3️⃣ Does it use neither? → Yes → Static method

<br>

## Comparison Table
| Feature                           | Instance Method | Static Method | Class Method |
| --------------------------------- | --------------- | ------------- | ------------ |
| First Parameter                   | `self`          | none          | `cls`        |
| Access instance attributes        | ✔               | ✘             | ✘            |
| Access class attributes           | ✔               | ✘             | ✔            |
| Modify class attributes           | Indirectly      | ✘             | ✔            |
| Used for alternative constructors | ✘               | ⚠ (not ideal) | ✔            |


