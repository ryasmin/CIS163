**Exercise 1:** Rewrite the following code snippets using list comprehensions.

```
fruits = [` apple', `banana ', `kiwi ']

for i in range(len(fruits)):
  fruits[i] = fruits[i].strip()
```

</br>

```
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]

newlist = []

for x in fruits:
  if "a" not in x:
    newlist.append(x)
```

</br>

```
lst1 = [1, 2, 3]
lst2 = [3, 4, 5]

result = []
for i in lst1:
  for j in lst2:
    result.append((i, j))
```

</br>

```
lst1 = [1, 2, 3]
lst2 = [3, 4, 5]

result = []
for i in lst1:
  for j in lst2:
    if i != j:
      result.append((i, j))
```

</br>

```
vec = [[1, 2, 3], [4, 5, 6]]

new_vector = []
for i in range(len(vec)):
  for j in range(len(vec[i])):
    new_vector.append(vec[i][j])
```

</br>

```
vec = [[1, 2, 3], [4, 5, 6]]

new_vector = []

for v in vec:
  for item in v:
    new_vector.append(item)
```

</br>

**Exercise 2:** Consider the following list:
```
fruits = ["apple", "banana", "mango", "cherry", "kiwi"]
```
Using list comprehension:
- Capitalize the first letter of each word in the list.
- Only keep the names with exactly five characters.
- Make a list containing the number of characters in each fruit.

</br>

**Exercise 3:** Consider the following list:
```
nums = [1, -5, 7, 9, -15]
```
Using list comprehension:
- Add 1 to each number in the list.
- Only keep the positive numbers.
- Only keep the negative numbers.
