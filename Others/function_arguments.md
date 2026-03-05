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

This prevents mistakes when there are many parameters.
```python
def print_date(day, month, year):
  print(f"{month}/{day}/{year}")

print_date(3, 15, 2026)
print_date(month=3, day=15, year=2026)
```

Advantages of Keyword Arguments
- More readable
- Order does not matter
- Useful when functions have many parameters


> You can combine both positional and keyword arguments, but positional arguments must come first.

```python
checkout("Alice", item="Laptop", price=1200)
print_date(3, day=15, year=2026)
```

Invalid 🚫:
```
checkout(customer="Alice", "Laptop", 1200)
print_date(day=15, 3, year=2026)
```

<br>

## Variable Number of Positional Arguments: `*args`

Sometimes you don't know how many arguments a function will receive. Instead of forcing users to create a list, we can allow any number of positional arguments.

Example: Chekout with Multiple Items
```python
def checkout(*items):
    print("Items purchased:")
    for item in items:
        print("-", item)

checkout("apple", "banana", "milk")
checkout("mango", "kiwi")
```

Here `*items` collects all positional arguments into a tuple.
```python
items = ("apple", "banana", "milk")
items = ("mango", "kiwi")
```

Python's built-in `print()` function works the same way.
```python
print("Hello", "world", "!")
```

<br>

## Variable Number of Keyword Arguments: `**kwargs`

`**kwargs` allows functions to accept any number of named arguments.

```python
def checkout(customer, *items, **details):

    print("Customer:", customer)

    print("Items :")
    for item in items:
        print("-", item)

    print("Order details:")
    for key, value in details.items():
        print(f"{key}: {value}")
```

Here `**info` collects all keyword arguments into a dictionary.
```python
info = {
  "name": "Alice",
  "age": 25,
  "city": "Chicago"
}
```

```python
def create_account(username, **details):
    print(f"Creating account for {username}")
    
    for key, value in details.items():
        print(f"{key}: {value}")

create_account("john123", email="john@email.com", country="USA")
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
