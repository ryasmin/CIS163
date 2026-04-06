## Level: Moderate

### Tree Recursion (Two Branches)
> Each recursive call splits into two subproblems (decision-based recursion)

#### Exercise 1: Fibonacci Sequesnce
Write a recursive function that takes a non-negative integer `n` and returns the `n`-th Fibonacci number.
```
fib(n = 4) -> 3
```

#### Exercise 2: Count Unique Paths on Stairs
Write a recursive function that takes an integer `n` representing the number of steps and returns the number 
of distinct ways to reach the top. You may only take either one or two steps at a time.
```
path_stairs(n = 5) -> 8
```

#### Exercise 3: Count Unique Paths on a Grid
Write a recursive function that takes two integers `r` and `c`, representing the number of rows and columns in a grid, 
and returns the number of unique paths from the top-left corner to the bottom-right corner. You may only move either right or down at each step.
```
path_grid(r = 4, c = 4) -> 20
```

<br>

### Optimization with Memoization
> Avoid repeated computation in recursion trees.
General Structure:
```
def function_name(param1, param2, ...., memo = {}):
  # Base Case
  .....
  if (param1, ...) in memo:
    return memo[(param1, ...)]
  memo[(param1, ...)] = recursive problem(s)
  return memo[(param1, ...)]
```

#### Exercise 4: Solving using Memoization
Solve Exercises 1-3 using memoization.

<br>

### Generative Recursion (Include / Exclude Pattern)
> At each step, decide whether to include or exclude an element

#### Exercise 5: Generate All Subsequences (Print only)
Write a recursive function that takes a string (`s`) and prints all possible subsequences of the string.

#### Exercise 6: Return All Subsequences
Write a recursive function that takes a string (`s`) and returns a list containing all possible subsequences of the string.

#### Exercise 7: Return All Subarrays
Write a recursive function that takes a list (`lst`) and returns all possible subarrays of the list.

#### Exercise 8: Subarrays with Sum `k`
Write a recursive function that takes a list of integers (`lst`) and a target value `k`, and returns all subsets of the list whose sum is equal to k.


