## Mystery Testing (Reverse Engineering)

```python
def mystery(n):
    if type(n) != int:
        raise TypeError
    if n < 0:
        raise ValueError
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True
```

__Tasks__: Without being told what it does:

1. Create at least 6 tests that determine its behavior.
2. Include:
    - normal cases
    - edge cases
    - exception cases
3. Write one sentence: “I believe this function does ______.”
