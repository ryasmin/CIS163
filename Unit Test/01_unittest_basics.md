# Unit Testing in Python with unittest

Reference: Python unittest docs: https://docs.python.org/3/library/unittest.html

__Unittest:__ A unit test is a small program that checks whether a single function or method behaves correctly.

When testing a function, you generally want test cases from these categories:
1. Typical inputs (normal case)
2. Edge cases (boundary values)
3. Invalid inputs (should raise errors)

<br>

## Minimum Working `unittest` Template

#### Step 1 — Write a function to test
```python
def add(a, b):
    return a + b
```

#### Step 2 — Create a test class
Rules:
- Import `unittest`
- Test class must inherit from `unittest.TestCase`
- Test methods must start with `test_...`

```python
import unittest

class TestAdd(unittest.TestCase):
    def test_add_positive(self):
        self.assertEqual(add(1, 2), 3)
```

#### Step 3 — Run the tests
```python
if __name__ == "__main__":
    unittest.main()
```

#### Example 1: testing `add` with categories
```python
class TestAdd(unittest.TestCase):

    def test_add_positive(self):
        self.assertEqual(add(2, 3), 5)

    def test_add_negative(self):
        self.assertEqual(add(-2, -3), -5)

    def test_add_mixed(self):
        self.assertEqual(add(2, -3), -1)
```
__TO DO:__ Write 3 more tests for add:
- `add(0, 0)`
- `add(0, 5)`

<br>

## Splitting Code into Files
In real projects you usually have two seperate files:
1. Code you want to test
2. Code with your test cases

#### Example 2
`calc.py`
```python
def add(x, y):
    return x + y

def subtract(x, y):
    return x - y
```

`text_calc.py`
```python
import unittest
import calc

class TestCalc(unittest.TestCase):

    def test_add(self):
        self.assertEqual(calc.add(10, 5), 15)
        self.assertEqual(calc.add(-1, 1), 0)

    def test_subtract(self):
        self.assertEqual(calc.subtract(5, 2), 3)
        self.assertEqual(calc.subtract(2, 5), -3)
        self.assertEqual(calc.subtract(-5, -2), -3)
        self.assertEqual(calc.subtract(-5, 2), -8)
        self.assertEqual(calc.subtract(5, -2), 7)

if __name__ == "__main__":
    unittest.main()
```
__Note:__
- In Example 1, we created seperate test functions for each test case of `add`.
- In Example 2, we put all test cases in the same test function.

__Question:__
- What are the differences in output?
- Which should be used when?
- What is the difference between `import calc` and `from calc import add, subtract`?

<br>

## Reducing Repetition: `subTest` for Multiple Cases
Instead of copy/pasting many assertEqual calls, you can loop through cases and use subTest so failures show which case failed.

```python
class TestCalculator(unittest.TestCase):

    def test_add_cases(self):
        cases = [
            (3, 2, 5),
            (-1, 1, 0),
            (-2, -5, -7)
        ]

        for a, b, expected in cases:
            with self.subTest(a=a, b=b, expected=expected):
                self.assertEqual(add(a, b), expected)
```

<br>

## Testing Exceptions Correctly
When a function is supposed to reject bad input, tests should confirm it raises the right exception.

```python
def divide(x, y):
    if y == 0:
        raise ValueError("Cannot divide by zero!")
    return x / y
```

There are two common styles:

1. __Style A — `assertRaises` as context manager__
    ```python
    with self.assertRaises(ValueError):
        divide(10, 0)
    ```

2. __Style B — `assertRaises(ExceptionType, func, args1, args2, ...)`__
    ```python
    self.assertRaises(ValueError, divide, 10, 0)
    ```

#### Example 3: Password Validator
This function checks if a password meets several requirements.
```python
def validate_password(password):
    """
    Validates a password based on several rules.

    Rules:
    - Must be a string
    - Must be at least 8 characters long
    - Must contain at least one digit
    - Must contain at least one uppercase letter
    """

    if not isinstance(password, str):
        raise TypeError("Password must be a string.")

    if len(password) < 8:
        raise ValueError("Password must be at least 8 characters long.")

    if not any(char.isdigit() for char in password):
        raise ValueError("Password must contain at least one digit.")

    if not any(char.isupper() for char in password):
        raise ValueError("Password must contain at least one uppercase letter.")

    return True
```

__TO DO:__
- Write your own test case to make sure each exception is raised properly.

<br>

## Floating-Point Testing: Use `assertAlmostEqual`
Floating-point results can differ slightly due to how computers store decimals.
So you often test with tolerance.

```
self.assertAlmostEqual(0.1 + 0.2, 0.3, places=7)
```

#### Example 4: Sales Tax Calculation
```python
def calculate_total(price, multiplier):
    return price * multiplier

price = 0.1
multiplier = 0.2
total = calculate_total(price, multiplier)
```
You would expect `0.02`, but python actually produces `0.020000000000000004`.

Similarly,
```
print(0.1 + 0.2)                # Output: 0.30000000000000004
print((0.1 + 0.2) == 0.3)       # Output: False
```

The following test will fail with `assertEqual`:
```python
import unittest

class TestTax(unittest.TestCase):

    def test_total(self):
        result = calculate_total(0.1, 0.2)
        self.assertEqual(result, 0.02)
```

Output:
```
AssertionError: 0.12000000000000001 != 0.02
```

Correct Test using `assertAlmostEqual`:
```python
class TestTax(unittest.TestCase):

    def test_total(self):
        result = calculate_total(0.1, 0.2)
        self.assertAlmostEqual(result, 0.12, places=7)
```
