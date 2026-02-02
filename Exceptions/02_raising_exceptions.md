# Raising Exceptions

The `raise` statement allows you to force a specified exception to occur. 

Useful for:
- enforcing rules and
- validating inputs.

---

### Example 1: Raising an Exception
```
age = int(input("Enter your age: "))

if age < 0:
    raise ValueError

print("Age accepted.")
```
---

### Example 2: Raising and Catching an Exception
```
try:
  age = int(input("Enter your age: "))
  
  if age < 0:
      raise ValueError
  
  print("Age accepted.")

except ValueError:
  print("Age cannot be negative.")
```
---

### Example 3: Raising and Catching an Exception with `as e`
```
try:
  age = int(input("Enter your age: "))
  
  if age < 0:
      raise ValueError("Age cannot be negative.")
  
  print("Age accepted.")

except ValueError as e:
  print(e)
```
