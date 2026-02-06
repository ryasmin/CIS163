## Step 0 – Starter class (the “anchor”)

```
class Order:
    def __init__(self, order_id: int):
        self.order_id = order_id

    def total_price(self):
        # For now, just return 0.0 – we’ll make this meaningful later
        return 0.0

o1 = Order(1)
print(o1.total_price())
```

> __Question:__ In this world so far, what does an Order object know about, or ‘hold on to’ inside itself?

> __Answer:__ just `order_id`.

## Step 1 – Customer Class

```
class Customer:
    def __init__(self, customer_id: int, name: str):
        self.customer_id = customer_id
        self.name = name
```

> __Question:__ How would you create a connection between `Customer` and `Order`?

Each Customer can have multiple Orders.

```
class Customer:
    def __init__(self, customer_id: int, name: str):
        self.customer_id = customer_id
        self.name = name
        self.orders: list[Order] = []

    def add_order(self, order: "Order") -> None:
        self.orders.append(order)
```

Each Order should be associated with a specific Customer.

```
class Order:
    def __init__(self, order_id: int, customer: Customer):
        self.order_id = order_id
        self.customer = customer

    def total_price(self) -> float:
        return 0.0
```

> __Questions:__
> 1. Does Customer contains/uses Order?
> 2. Does Order contains/uses Customer?
> 3. Are these relationships temporary/ long-term?

## Step 2 – LineItem Class

```
class LineItem:
    def __init__(self, product_name: str, unit_price: float, quantity: int):
        self.product_name = product_name
        self.unit_price = unit_price
        self.quantity = quantity

    def line_total(self) -> float:
        return self.unit_price * self.quantity
```

> __Question:__ How would you create a connection between `LineItem` and `Order`?

```
class Order:
    def __init__(self, order_id: int, customer: Customer):
        self.order_id = order_id
        self.customer = customer
        self.items: list[LineItem] = []

    def add_item(self, item: LineItem) -> None:
        self.items.append(item)

    def total_price(self) -> float:
        return sum(item.line_total() for item in self.items)
```
> __Questions:__
> 1. Does LineItem contains/uses Order?
> 2. Does Order contains/uses LineItem?
> 3. Are these relationships temporary/ long-term?

## Step 5 – Relationship via Method Parameter

```
class TaxCalculator:
    def calculate_tax(self, subtotal: float) -> float:
        # Very simple fake tax rule: 10% tax
        return subtotal * 0.10
```
> __Questions:__ What type of relationship?

```
class Order:
    # ... existing __init__, add_item, total_price, etc.

    def total_with_tax(self, tax_calculator: TaxCalculator) -> float:
        subtotal = self.total_price()
        tax = tax_calculator.calculate_tax(subtotal)
        return subtotal + tax
```

Step 6 – Relationship via Local-variable

```
class InvoiceFormatter:
    def format(self, order: Order) -> str:
        lines = [f"Invoice for {order.customer.name} (Order #{order.order_id})"]
        for item in order.items:
            lines.append(
                f"- {item.product_name}: {item.quantity} x {item.unit_price:.2f} "
                f"= {item.line_total():.2f}"
            )
        lines.append(f"Total: {order.total_price():.2f}")
        return "\n".join(lines)
```

```
class Order:
     # ... existing __init__, add_item, total_price, etc.

    def generate_invoice_text(self) -> str:
        formatter = InvoiceFormatter()
        return formatter.format(self)
```



