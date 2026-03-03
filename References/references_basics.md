# Variables Store References, Not Objects

In Python:
- A variable does NOT store the object itself.
- A variable stores a reference (address) to the object.

The address can be retrieved using the `id()` function.

```
x = 3000
y = 3000
print(id(x))      # Example Output: 140564025048944
print(id(y))      # Example Output: 140564025360880
```

Each `3000` is a new instance of the `int` class. 

#### Small-int "Exception"
```
x = 5
y = 5
print(id(x))      # Example Output: 11654504
print(id(y))      # Example Output: 11654504
```

- __Note:__
    - Unlike previous example, both `x` and `y` are referencing the same object.
- __Explanation:__
    - CPython (the standard Python implementation) pre-creates small integers, typically from -5 to 256, to optimize performance.
    - That means these integer objects are created in advance and reused instead of being recreated each time.

<br>

## Mutable vs Immutable Objects

### 1. How references to ___Immutable___ objects work
```
x = 5
y = x
# ----- Step 1 -------
print(x, id(x))
print(y, id(y))

x = 10
# ----- Step 2 -------
print(x, id(x))
print(y, id(y))
```
___Explanation:___
- Reassignment: `5` (`int`) is immutable (cannot be modified in place), so need to create a new object `10`, not replace `5`.
- At Step 1
  ```
  x  ──> 5 <── y
  ```
- At Step 2:
    - `x` points to a new object (`10`)
    - `y` still points to `5`
   ```
   5 <── y
   x  ──> 10
   ```

### 2. How references to ___Mutable___ objects work
```
a = [1,2,3]
b = a
# ----- Step 1 -------
print(a, id(a))
print(b, id(b))

a.append(4)
# ----- Step 2 -------
print(a, id(a))
print(b, id(b))
```

___Explanation:___
- Mutation: `a` (`list`) is mutable (can be modified in place), so no need to create a new object.
- At Step 1
  ```
  a  ──> [1, 2, 3] <── b
  ```
- At Step 2:
    - `a` and `b` still points to the same object
   ```
   a  ──> [1, 2, 3, 4] <── b
   ```

<br>

## Function Arguments and Returns Are References
Python uses pass-by-assignment (sometimes loosely called pass-by-object-reference).

When you:
- pass an argument → the parameter name is bound to the same object
- return a value → the receiving variable is bound to the same object

No copying happens unless you explicitly create a new object.

> In Python function parameters receive references to objects, not copies of objects.

- Python DOES NOT pass variables.
- Python DOES NOT pass raw values.
- Python passes references to objects.

### 1. Immutable Example (Reassignment)
```
1. def modify(x):
2.     x = 10
3. 
4. a = 5
5. modify(a)
6. print(a)        # Output: 5
```

What Happens:
- Line 4:       `a ──> 5`
- Line 5 and 1: `a ──> 5 <── x`
- Line 2:       `a ──> 5,     x ──> 10`

### 2. Mutable Example (Mutation)
```
1. def modify(lst):
2.     lst.append(100)
3. 
4. a = [1, 2, 3]
5. modify(a)
6. print(a)
```

What Happens:
- Line 4:       `a ──> [1, 2, 3]`
- Line 5 and 1: `a ──> [1, 2, 3] <── lst`
- Line 2:       `a ──> [1, 2, 3, 100] <── lst`

### 3. Argument Passing Bug (Mutation vs Reassignment)
```
1. def clear_list(lst):
2.    lst = []   
3. 
4. numbers = [1, 2, 3]
5. clear_list(numbers)
6. print(numbers)
```

What Happens (Reassignment):
- Line 4:       `numbers ──> [1, 2, 3]`
- Line 5 and 1: `numbers ──> [1, 2, 3] <── lst`
- Line 2:       `numbers ──> [1, 2, 3]         lst ──> [] `

Correct Version (Mutation):
```
def clear_list(lst):
    lst.clear()
```

### 4. Return Value Bug (Aliasing Problem)
```
class Account:
    def __init__(self, balance):
        self.balance = balance

    def __add__(self, other):
        self.balance += other.balance
        return self

a1 = Account(100)
a2 = Account(50)
a3 = a1 + a2
a3.balance = 0
print(a1.balance)
```

What Happens:
- Inside `__add__`, `self.balance += other.balance` mutates `a1`:
      ```
      100 + 50 → a1.balance = 150
      ```
- Then `return self` returns a reference to the same object as `a1`.
<br>

## Default Mutable Argument Trap
```
def add_item(item, lst=[]):
    lst.append(item)
    return lst

print(add_item(1))    
print(add_item(2))
print(add_item(3))
```

Expected Output:
```
[1]
[2]
[3]
```

Actual Output:
```
[1]
[1, 2]
[1, 2, 3]
```

___The Key Rule___
> Default argument values are evaluated once, at function definition time. NOT each time the function is called.

What Happens:
- Call 1:
  ```
  lst ──> []
  append 1        lst ──> [1]
  ```
- Call 2:
  ```
  lst ──> [1]
  append 2        lst ──> [1, 2]
  ```
- Call 3:
  ```
  lst ──> [1, 2]
  append 3        lst ──> [1, 2, 3]
  ```

  Correct Version:
  ```
  def add_item(item, lst=None):
    if lst is None:
        lst = []
    lst.append(item)
    return lst
```
