## Food Delivery System

In this system, there is an interface named `Trackable`. Anything that is trackable must have a public `get_status(): str` method and a public `update_status(new_status: str)` method. 

There is an abstract class named `Delivery` that realizes (implements) `Trackable`. Every Delivery has a private string named `delivery_id`, a private string named `status`, and a public `estimate_time(): int` method. 

There are two subclasses of `Delivery`: `BikeDelivery` and `CarDelivery`, and each overrides `estimate_time()` differently. An `Order` class exists which is associated with exactly one `Customer` and contains a public list of `Item` objects named `items`. `Order` is also associated with exactly one `Delivery` (an order “has a delivery”). A `RoutePlanner` class is not stored inside any object, but `Delivery.estimate_time()` uses a `RoutePlanner` as a method parameter to compute an estimate.

<details>

<summary> Solution </summary>

```mermaid

```

</details>
