# Function Arguments in Python

## Positional Argument

A positional argument is assigned to a parameter based on its position in the function call.
```python
def checkout(customer, item, price):
    print(f"{customer} bought {item} for ${price}")
```

<br>

## Keyword Arguments

A keyword argument assigns values to parameters by name, not position.
```python
checkout(customer="Alice", item="Laptop", price=1200)
```

Advantages of Keyword Arguments
- More readable
- Order does not matter
- Useful when functions have many parameters

```python
def print_date(day, month, year):
  print(f"{month}/{day}/{year}")

print_date(3, 15, 2026)
print_date(month=3, day=15, year=2026)
```

> You can combine both positional and keyword arguments, but positional arguments must come first.

```python
checkout("Alice", item="Laptop", price=1200)
print_date(3, day=15, year=2026)
```

🚫 Invalid Calls:
```python
checkout(customer="Alice", "Laptop", 1200)
print_date(day=15, 3, year=2026)
```

<br>

## Variable Number of Positional Arguments: `*args`

Sometimes you don't know how many arguments a function will receive. 
Instead of forcing users to create a list, we can allow any number of positional arguments.

#### Example: Checkout with Multiple Items
```python
def checkout(*items):
    print("Items purchased:")
    for item in items:
        print("-", item)

checkout("Laptop", "Mouse", "Keyboard")
checkout("Laptop", "Mouse")
```

Here `*items` collects all positional arguments into a tuple inside the function.
```python
items = ("Laptop", "Mouse", "Keyboard")
items = ("Laptop", "Mouse")
```

Python's built-in `print()` function works the same way.
```python
print("Hello", "world", "!")
```

<br>

## Variable Number of Keyword Arguments: `**kwargs`

`**kwargs` allows functions to accept any number of named arguments.

```python
def checkout(**details):
    print("Order details:")
    for key, value in details.items():
        print(f"{key}: {value}")

checkout(payment="Credit Card", shipping="Express")
checkout(payment="Credit Card", shipping="Express", state="Michigan")
```

Here `**details` collects all keyword arguments into a dictionary.
```python
details = {"payment"="Credit Card", "shipping"="Express"}
details = {"payment"="Credit Card", "shipping"="Express", "state"="Michigan"}
```

## Using *args and **kwargs Together

You can combine them in a function.
```python
def order_summary(customer, *items, **details):
    print("Customer:", customer)

    print("Items:")
    for item in items:
        print("-", item)

    print("Details:")
    for key, value in details.items():
        print(f"{key}: {value}")

order_summary(
    "Alice",
    "Laptop",
    "Mouse",
    payment="Credit Card",
    shipping="Express"
)
```
__Order of Parameters:__
- regular arguments
- *args
- **kwargs
