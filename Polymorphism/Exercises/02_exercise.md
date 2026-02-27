Consider a shopping cart system. There are three purchasable types:
1. PhysicalProduct
2. DigitalProduct
3. Subscription

```
class PhysicalProduct:
    def __init__(self, name, price, shipping_cost):
        self.name = name
        self.price = price
        self.shipping_cost = shipping_cost

class DigitalProduct:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class Subscription:
    def __init__(self, name, monthly_fee, months):
        self.name = name
        self.monthly_fee = monthly_fee
        self.months = months


def calculate_total(item):
    if isinstance(item, PhysicalProduct):
        return item.price + item.shipping_cost
    elif isinstance(item, DigitalProduct):
        return item.price
    elif isinstance(item, Subscription):
        return item.monthly_fee * item.months
    else:
        raise TypeError("Unsupported item type")


cart = [
    PhysicalProduct("Laptop", 1000, 25),
    DigitalProduct("Ebook", 20),
    Subscription("Streaming", 10, 6)
]

total = 0
for item in cart:
    total += calculate_total(item)

print("Total:", total)
```

### Task
1. Rrefactor the design so that `calculate_total` does not need to know the concrete types of the objects passed
   and does not use `isinstance`.
2. What are the advantages of the new design?
3. Use Operator Overloading, i.e., `__add__` to sum the total cost of two copies of the same Laptop.
4. Use Operator Overloading, i.e., `__mul__` to get the price of 4 copies of the same Laptop.
5. Use Operator Overloading, i.e., `__add__` to sum the total cost of the first two items in `cart`.
6. Use Operator Overloading, i.e., `__add__` to sum the total cost of the three items in `cart`.
7. Add `__eq__` so that two products are equal if their total purchase prices are the same.
