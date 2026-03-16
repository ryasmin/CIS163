## Unittest Exercise
Write unit tests for the function below using Python’s `unittest` module.
```python
def calculate_shipping(weight, distance, is_express=False):
    """
    Calculates shipping cost.

    Rules:
    - weight must be positive
    - distance must be positive
    - base price = $5
    - cost per kg = $1.2
    - cost per km = $0.05
    - express shipping adds 50% to the final cost

    Returns the total shipping cost.
    """

    if not isinstance(weight, (int, float)):
        raise TypeError("Weight must be numeric.")

    if not isinstance(distance, (int, float)):
        raise TypeError("Distance must be numeric.")

    if weight <= 0:
        raise ValueError("Weight must be positive.")

    if distance <= 0:
        raise ValueError("Distance must be positive.")

    cost = 5 + (1.2 * weight) + (0.05 * distance)

    if is_express:
        cost *= 1.5

    return cost
```

__Hints:__ Your tests should cover the following scenarios:

- Normal cases (use `assertAlmostEqual` since floating point value)
    - Positive `weight` and `distance` with `is_express=False`
    - Positive `weight` and `distance` with `is_express=True`
- Type validation (use `assertRaises`): Non-numeric `weight` or `distance`
- Value validation (use `assertRaises`): `weight <= 0` or `distance <= 0`
- Logical correctness
    - Verify that the returned shipping cost is always positive
    - Use `assertTrue` with `cost > 0`.
