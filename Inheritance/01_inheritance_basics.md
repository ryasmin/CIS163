# Inheritance

Inheritance allows one class to reuse code from another class.

It helps us avoid repetition and makes programs easier to maintain.

In Inheritance:
1. __Base/Parent/Super Class__ $\rightarrow$ The class whose attributes and behaviors other classes can reuse.
2. __Derived/Child/Sub Class__ $\rightarrow$ The class that inherits attributes and behaviors from another class.

<br>

## IS-A Relationship
Inheritance models an “IS-A” relationship between classes.

   > $$\text{Class A "IS-A" Class B}$$

If this sentence makes sense $\Rightarrow$ then inheritance is appropriate.

Example:
- `Dog` IS-AN `Animal` $\Rightarrow$ ✔️ inheritance makes sense
- `Car` IS-AN `Engine` $\Rightarrow$ ✖️ should probably not be inheritance

<br>

## Creating Inheritance Relationship

### Step 1 — Base Class
Suppose a company has employees. Every employee has:
- first name
- last name
- email

> Our Parent/ Base Class
```python
class Employee:
    def __init__(self, first, last):
        self.first = first
        self.last = last

    def email(self):
        return f"{self.first.lower()}.{self.last.lower()}@company.com"

emp1 = Employee("John", "Doe")
print(emp1.email())              # Output: john.doe@company.com
```



<br>

### Step 2 — Problem Without Inheritance
Now suppose we have two types of employees:
- Salary employees
- Hourly employees

Bad design (repetition):
```python
class SalaryEmployee:
    def __init__(self, first, last, salary):
        self.first = first
        self.last = last
        self.salary = salary

    def email(self):
        return f"{self.first.lower()}.{self.last.lower()}@company.com"


class HourlyEmployee:
    def __init__(self, first, last, hours, rate):
        self.first = first
        self.last = last
        self.hours = hours
        self.rate = rate

    def email(self):
        return f"{self.first.lower()}.{self.last.lower()}@company.com"
```

__Problem:__
- Attributes repeated: `first` and `last`
- Methods repeated: `email`
- not DRY (Do Not Repeat Yourself)

We fix this using inheritance.

<br>

### Step 3 — Basic Inheritance

Child class syntax:
```
class Child(Parent):
```

> We resuse `Employee`

```python
class SalaryEmployee(Employee):
    pass

class HourlyEmployee(Employee):
    pass

emp1 = SalaryEmployee("John", "Doe")
emp2 = HourlyEmployee("Jane", "Smith")

print(emp1.email())        # Output: john.doe@company.com
print(emp2.email())        # Output: jane.smith@company.com
```

__Lookup Diagram — Constructor__

```
emp1 = SalaryEmployee("John", "Doe")

Look in SalaryEmployee for __init__
        ↓
✖️ NO __init__ in SalaryEmployee
        ↓
🔼 Go to parent (Employee)
        ↓
Employee.__init__ runs
        - self.first = "john" (emp1.first)
        - self.last  = "doe"  (emp1.last)
```

__Lookup Diagram — `email()`__
```
emp1.email()

Look in SalaryEmployee for email
        ↓
✖️ NO email in SalaryEmployee
        ↓
🔼 Go to parent (Employee)
        ↓
Employee.email runs
         - Use emp1.first and emp1.last
         - Return "john.doe@gmail.com"
```
<br>

### Step 4 — Adding New Attributes to Child

Salary employee needs a new `salary` attribute. We want to reuse parents's `__init__` method and add salary on top of it.

> Use `super()`

```python
class SalaryEmployee(Employee):
    def __init__(self, first, last, salary):
        super().__init__(first, last)
        self.salary = salary

    def payroll(self):
        return self.salary

emp1 = SalaryEmployee("John", "Doe", 1000)

print(emp1.email())
print(emp1.payroll())
```

__Object Creation Trace__
```
emp1 = SalaryEmployee("John", "Doe", 1000)

Look in SalaryEmployee for __init__
        ↓
SalaryEmployee has its own __init__
        ↓
Run SalaryEmployee.__init__
        ↓
super() means go to the parent class (Employee)
        ↓
Run Employee.__init__(first, last)
         - self.first = "John"
         - self.last = "Doe"
        ↓
Continue SalaryEmployee.__init__
         - self.salary = 1000
```

Final object `emp1` has:
- `self.first = "John"`
- `self.last = "Doe"`
- `self.salary = 1000`

<br>

### Step 5 — Another Child Class

```python
class HourlyEmployee(Employee):
    def __init__(self, first, last, hours, rate):
        super().__init__(first, last)
        self.hours = hours
        self.rate = rate

    def payroll(self):
        return self.hours * self.rate

emp2 = HourlyEmployee("Jane", "Smith", 40, 20)

print(emp2.email())
print(emp2.payroll())
```

Final object `emp2` has:
- `self.first = "Jane"`
- `self.last = "Smith"`
- `self.hours = 40`
- `self.rate = 20`


<br>

### Step 6 — Child of Child
A class can inherit from another child.

Example:

&nbsp;&nbsp;&nbsp;Commission employee = salary + bonus

Instead of   `Employee —> CommissionEmployee`, we do:
> `Employee —> SalaryEmployee —> CommissionEmployee`

```python
class CommissionEmployee(SalaryEmployee):
    def __init__(self, first, last, salary, commission):
        super().__init__(first, last, salary)
        self.commission = commission

    def payroll(self):
        base = super().payroll()
        return base + self.commission
```
Here we used `super()` twice:
- to call parent's (`SalaryEmployee`) constructor
- to call parent's `payroll` method

__Lookup Diagram — Constructor__
```
emp3 = CommissionEmployee("John", "Doe", 1000, 300)

CommissionEmployee.__init__
        ↓ super()
SalaryEmployee.__init__
        ↓ super()
Employee.__init__
   self.first = "John"
   self.last  = "Doe"
        ↓
SalaryEmployee.__init__ continues
   self.salary = 1000
        ↓
CommissionEmployee.__init__ continues
   self.commission = 300
```

__Lookup Diagram — `email()`__
```
emp3.email()

CommissionEmployee
    ↓ no email
SalaryEmployee
    ↓ no email
Employee.email
    ↓
use first + last
```

__Lookup Diagram — `payroll()`__
```
emp3.payroll()

CommissionEmployee.payroll
    ↓ super()
SalaryEmployee.payroll
   return self.salary = 1000
    ↓
CommissionEmployee.payroll continues
   base  = 1000
   return base + self.commission = 1000 + 300 = 1300
```

<br>

### Step 7 — Protected Attributes

Sometimes we want attributes to be used by child classes, but not by outside code.

Using private visibility doesn't work (double underscore `__`), since even child cannot access them.

> Use single underscore `_`

```python
class Employee:
    def __init__(self, first, last, salary):
        self.first = first
        self.last = last
        self._salary = salary   # protected

class BonusEmployee(Employee):
    def __init__(self, first, last, salary, bonus):
        super().__init__(first, last, salary)
        self.bonus = bonus

    def total_pay(self):
        return self._salary + self.bonus
```

__Note:__ `emp._salary` can be accessed from outside, but is considered bad practice. SHOULD only be used by child class.

<br>

### Step 8 — Protected Method

Similarly can also create protected methods.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self._salary = salary

    def _base_pay(self):
        return self._salary

class BonusEmployee(Employee):
    def __init__(self, name, salary, bonus):
        super().__init__(name, salary)
        self.bonus = bonus

    def total(self):
        return self._base_pay() + self.bonus
```
