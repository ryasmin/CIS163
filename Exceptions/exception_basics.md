# Exception Handling 

### Common Built-In Exceptions
- `ZeroDivisionError`: Dividing a number by zero: `x = 10/0`.
- `NameError`: A local or global name is not found.
- `TypeError`: An operation or function is applied to an object of an inappropriate type: `2 + '2'`.
- `ValueError`: A function receives an argument that has the right type ___but___ an inappropriate value: `float('two')`.
- `IndexError`:	An index of a sequence does not exist: `x = [1, 2, 3], x[3]`.
- `KeyError`:	A key does not exist in a dictionary: `x = {1: 'h', 2: 'i'}, x['h']`.
- `ImportError`: An imported module or name cannot be found.
- `FileNotFoundError`: A file or directory is requested but does not exist. 

---

### Keywords
Python provides four keywords for handling exceptions: 

| **Keyword** | Description |
|---|---|
| `try` | Contains the code that might raise an exception |
| `except` | Catches and handles specific exceptions that occur in the `try` block |
| `else` | Executes only if no exception was raised in the `try` block |
| `finally` | Executes regardless of whether an exception occurred; often used for cleanup actions (e.g., closing files) |

---

### Syntax
```
try:
    # Code 
except SomeException:
    # Code
except:
    # Code 
else:
    # Code 
finally:
    # Code
```

---

### Example

```
try:
    num = int(input("Enter a number: "))
    den = int(input("Enter a number: "))
    result = num / den
    print(f"Result: {result}")

except ValueError:
    print("ValueError.")
    print("Please enter valid integers.")

except ZeroDivisionError:
    print("ZeroDivisionError.")
    print("Division by zero is not allowed")

except Exception:
    print("Unexpected Error.")

else:
    print("Calculation completed successfully.")

finally:
    print("Program finished.")
```
---

### Using `as e` with Built-in Exceptions

For built-in exceptions automatically raised by Python, using `as e` allows you to capture and display the system-generated error message. 

Useful for:
- debugging,
- logging, or
- providing more detailed feedback.

___Note:___ `e` is just a placeholder variable name. Any valid variable name can be used. Although `e` or `exp` is the most widely used by convention.

```
try:
    num = int(input("Enter a number: "))
    den = int(input("Enter a number: "))
    result = num / den
    print(f"Result: {result}")

except ValueError as e:
    print(f"ValueError: {e}.")
    print("Please enter valid integers.")

except ZeroDivisionError as e:
    print(f"ZeroDivisionError: {e}.")
    print("Division by zero is not allowed")

except Exception as e:
    print(f"Unexpected Error: {e}.")
```
