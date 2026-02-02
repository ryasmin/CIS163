# Exception Tracing: Exercise 01
```
def parse_positive_int():
    s = input("Enter a positive integer: ")
    print("Step 1: Got raw input:", s)

    # This line may raise a built-in ValueError
    n = int(s)
    print("Step 2: Converted to int:", n)

    # This line may raise a forced (manual) ValueError
    if n <= 0:
        raise ValueError("Number must be positive.")

    print("Step 3: Value is positive")
    return n


try:
    result = parse_positive_int()
    print("Step 4: Final result:", result)

except ValueError as e:
    print("Caught ValueError in except block:", e)
```

__Task:__ Fill out the following table:

| Input   | Does `int(s)` succeed? | Where does the error happen? | Built-in or forced? | Message printed in `except` block |
| ------- | ---------------------- | ---------------------------- | ------------------- | --------------------------------- |
| `"10"`  |                        |                              |                     |                                   |
| `"-3"`  |                        |                              |                     |                                   |
| `"0"`   |                        |                              |                     |                                   |
| `"abc"` |                        |                              |                     |                                   |
