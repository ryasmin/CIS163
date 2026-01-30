## **List Comprehension**

A compact way to create a new list from an existing sequence in a single line of code. It combines 
- `for-loop`(s) and
- conditional statements (`if-condition`)

directly inside a single square bracket `[]`.

</br>

### **Basic Syntax**
```
new_list = [expression for item in iterable if condition == True]
```
</br>

### **Steps**
- Step 1: Start with a good loop: make an empty list, then append.

Example: Suppose we want the squares of the even numbers from nums.
```
nums = [1, 2, 4, 5, 6, 9]

result = []
for n in nums:
    if n % 2 == 0:         # filter step
        result.append(n*n) # transform step
```
You can clearly see the filter `(if n % 2 == 0)` and the expression `(n*n)` being collected. This mapping makes the next step easier.

- Step 2: Translate to a list comprehension using the standard mapping.

Example:
1. Appended expression → `n*n` → goes in front
2. Loop → `for n in nums` → goes in the middle
3. Filter → `if n % 2 == 0` → goes to the end

</br>

### **Translation Cheat-Sheet**

- Simple Map (NO Filter)

Loop version
```
result = []
for x in items:
    result.append(f(x))
```

List comprehension
```
result = [f(x) for x in items]
```

- Map + Filter

Loop version
```
result = []
for x in items:
    if keep(x):
        result.append(f(x))
```

List comprehension
```
result = [f(x) for x in items if keep(x)]
```

- Nested Loops

Loop version
```
pairs = []
for a in A:
    for b in B:
        pairs.append((a, b))
```

List comprehension
```
pairs = [(a, b) for a in A for b in B]
```
