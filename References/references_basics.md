## Variables Store References, Not Objects

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

#### Exception:
```
x = 5
y = 5
print(id(x))      # Example Output: 11654504
print(id(y))      # Example Output: 11654504
```

- __Note:__
    - Unlike previous example, both `x` and `y` are referencing the same object.
- __Explanation:__
    - Python precreates small integers from -5 to 256 to optimize performance.
    - That means these integer objects are created in advance and reused instead of being recreated each time.

<br>

### Mutable vs Immutable Objects

#### How references to ___Immutable___ obejcts work
```
x = 5
y = x
# ----- Step 1 -------
print(x, id(x))
print(y, id(y))

x = 10
# ----- Step 1 -------
print(x, id(x))
print(y, id(y))
```
___Explanation:___
- Reassignment: `5` (`int`) is immutable (cannot be changed), so need to create a new object `10`, not replace `5`.
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

#### How references to ___Mutable___ obejcts work
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
- Mutation: `a` (`list`) is mutable (can be modified), so no need to create a new object.
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

### Function Arguments Are References
> In Python function parameters receive references to objects, not copies of objects.

- Python DOES NOT pass variables.
- Python DOES NOT pass raw values.
- Python passes references to objects.

#### Immutable Example
```
1. def modify(x):
2.     x = 10
3. 
4. a = 5
5. modify(a)
6. print(a)        # Output: 5
```

What Happens (Reassignment):
- Line 4:       `a ──> 5`
- Line 5 and 1: `a ──> 5 <── x`
- Line 2:       `a ──> 5,     x ──> 10`

#### Mutable Example
```
1. def modify(lst):
2.     lst.append(100)
3. 
4. a = [1, 2, 3]
5. modify(a)
6. print(a)
```

What Happens (Mutation):
- Line 4:       `a ──> [1, 2, 3]`
- Line 5 and 1: `a ──> [1, 2, 3] <── lst`
- Line 2:       `a ──> [1, 2, 3, 100] <── lst`

#### Reassignment with Mutable Types
```
def modify(lst):
    lst = [9, 9, 9]

a = [1, 2, 3]
modify(a)
print(a)
```

<br>

### Default Mutable Argument Trap
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

  Correct way to write it:
  ```
  def add_item(item, lst=None):
    if lst is None:
        lst = []
    lst.append(item)
    return lst
```
