## Level: Easy

### Return a Single Value
> Shrink the problem until base case is reached
> Return: current + recursion(smaller problem)

#### Exercise 1: Sum of Numbers
Write a recursive function that takes a non-negative integer (`n`) and returns the sum of positive numbers from 1 to `n`.
```
sum_nums(n = 4) -> 10 
```

#### Exercise 2: Factorial
Write a recursive function that takes a non-negative integer (`n`) and returns its factorial. The factorial is defined as:

$$n! = n \times (n-1) \times \cdots \times 1,\quad \text{with } 0! = 1$$
```
factorialn=(4) -> 24
```

#### Exercise 3: Reverse of a String
Write a recursive function that takes a string (`s`) and returns its reverse.
```
string_reverse(s="PIKA") -> "AKIP"
```

<br>

### Stop Early
> If Fail/Found return immediately OR continue recursion

#### Exercise 4: Check if Sorted
Write a recursive function that takes a list (`lst`) and returns `True` if the list is sorted in non-decreasing order, and `False` otherwise.
```
is_sorted(lst = [1, 3, 3, 6, 8]) -> True
is_sorted(lst = [1, 3, 6, 3, 8]) -> False
```

#### Exercise 5: Check Alternating Even and Odd
Write a recursive function that takes a list of integers (`lst`) and returns `True` if the list alternates between even and odd numbers
(starting from the first element), and `False` otherwise.
```
is_alternating([1, 2, 3, 4]) -> True
is_alternating([1, 3, 2, 4]) -> False
```

#### Exercise 6: First Uppercase Letter
Write a recursive function that takes a string (`s`) and returns the first uppercase letter in the string. 
If no uppercase letter exists, return `"Not Found"`.
```
firstUpper("gvSU") -> "S"
firstUpper("gvsu") -> "Not Found"
```

#### Exercise 7: First Uppercase Letter Index
Write a recursive function that takes a string and returns the index of the first uppercase letter in the string. 
If no uppercase letter exists, return `-1`.
```
firstUpperIndex("gvSU") -> 2
firstUpperIndex("gvsu") -> -1
```

#### Exercise 8: Sum of a List
Write a recursive function that takes a list of integers (`lst`) and returns the sum of all values in the given list.
```
sum_list(lst = [1, 3, 5]) -> 9
```

<br>

## Conditional Aggregation
> Include or skip based on condition
> Return: recursion(smaller problem) OR some value +  recursion(smaller problem)

#### Exercise 9: Sum of a List (Modified)
Write a recursive function that takes a list (`lst`) and returns the sum of all numeric values in the list. 
If an element is not of type `int` or `float`, ignore it and continue processing the remaining elements.
```
sum_numeric(lst = [4, "a", 3.5, 2]) -> 9
```

#### Exercise 10: Count Occurrence of Zeroes
Write a recursive function that takes a list (`lst`) and returns the number of zeroes in the list.
```
count_zeroes(lst = [1, 0, 3, 4, 0]) - > 0
```

#### Exercise 11: Count Occurrences of a Substring
Write a recursive function that takes a string (`s`) and a substring (`sub`), and returns the number of times the substring appears in the string.
```
count_substring("abaaa", "aa") -> 2
count_substring("baba", "bab") -> 1
```

<br>

### Return a New Data Structure
> Return: \[some value\]

#### Exercise 12: Identify Even Numbers in a List
Write a recursive function that takes a list (`lst`) and returns a new list containing only the even numbers from the given list.
```
collect_evens([1, 2, 3, 4, 5]) -> [2, 4]
collect_evens([1, 1, 3, 5, 7]) -> []
```

#### Exercise 13: Insert Separators between Elements
Write a recursive function that takes a list (`lst`) and a seperator (`sep`) and returns a new list 
where a given separator value is inserted between every pair of elements.
```
insert_separator([1, 2, 3], 0) -> [1, 0, 2, 0, 3]
insert_separator([1, 2, 3], '-') -> [1, '-', 2, '-', 3]
```
