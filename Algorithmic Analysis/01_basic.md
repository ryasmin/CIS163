## Introduction

When multiple programs solve the same problem, we need a way to decide which one is better.

We care about:
- How fast the program runs
- How well it scales as input size increases

There are two main ways to analyze algorithms:
1. **Time Complexity** -> How long a program takes to run
2. **Space Complexity** -> How much memory a program uses

In this course, we focus primarily on **Time Complexity**.

## Time Complexity
Time complexity describes how the number of operations grows as input size `n` increases.

We are NOT measuring exact time (seconds). Instead, we focus on **growth behavior**.

<br>

### 1. Constant Time — `O(1)`
An operation is O(1) if it takes the same time regardless of input size.

Examples (Python List Operations):
- `append()`
- `pop()`
- `lst[i]` (access value)
- `lst[i] = x` (update value)
> These use direct access, so they do not depend on list size.

<br>

### 2. Linear Time — `O(n)`
An algorithm is `O(n)` if it processes each element once.
```python
lst = [5, 7, 3]
for x in lst:
  print(x)
```
If we let `n = len(lst)`, this loop runs once for each element, so it performs $n$ operations.

---

#### Important Note: Not All Operations Are Equal
It Is easy to assume that every **built-in method** takes constant time, but that Is not always true.
To determine the actual time complexity, you need to think about what is happening behind the scenes. 
For example: 
```python
lst = [5, 7, 3]
lst.pop(0)
```
At first glance, this might look like a simple operation and therefore `O(1)`. What actually happens:
- Remove the first element:
  - `lst = [  , 7, 3]` - 1 operation
- Shift all remaining elements one position to the left to fill in the empty positions:
  - `lst = [7, , 3]`
  - `lst = [7, 3]`
  - This requires $n - 1$ operations.
- Total operations: $1 + n - 1 = n$
> So, `pop(0)` is `O(n)`, not `O(1)`.

---

<br>

### 3. Quadratic Time — O(n²)
Occurs usually when operations are nested.
```python
for i in range(n):
    for j in range(n):
        print(i, j)
```
- For each outer loop requires the inner loop runs $n$ times.
- $n$ outer loop.
- Total operations: $n \times n = n^2$
---

#### Important Note: Summation Patterns
Some algorithms don’t look like full nested loops but still behave similarly.
```python
for i in range(n):
    for j in range(i):
        print(i, j)
```
| Outer Loop (`i`) | Number of Inner Loop        | Operations |
|---------------|--------------------------------|------------|
| `i = 0`       | $0$                            | $0$        |
| `i = 1`       | $1$ (`j = 0`)                  | $1$        |
| `i = 2`       | $2$ (`j = 0, 1`)               | $2$        |
| ...           | ...                            | ...        |
| `i = n - 1`   | $n-1$ (`j = 0, 1, ..., n-2`)   | $n-1$      |

- Total Operations: $0 + 1 + 2 + ..... + (n-1) = \frac{n(n-1)}{2} = \frac{n^2}{2} - \frac{n}{2}$
---

<br>

### 4. Logarithmic Time — `O(logn)`
Logarithmic time with base 2 ($log_2 n$) occurs when the problem size is reduced by half in each step.

Example: Repeatedly dividing by 2
```python
n = 16
while n >= 1:
  n = n//2
```
- $16 \rightarrow 8 \rightarrow 4 \rightarrow 2 \rightarrow 1$
- For $n=16$, it takes 4 steps: $log_2n = log_216 = 4$

<br>

### 5. Exponential Time — `O(2ⁿ)`
Occurs when when the amount of work doubles at each step. 
This usually happens in recursive problems where each function call generates multiple new calls.

#### Example: Fibonacci Sequence
```python
               fib(4)
             ________|________
            |                 |
          fib(3)            fib(2)
        ____|____         ____|____
       |         |       |         |
     fib(2)    fib(1)  fib(1)    fib(0)
   ____|____
  |         |
fib(1)    fib(0)
```
- The recursion tree has $n=4$ levels
- At each level, each function call generate 2 new function calls.
- At each level, the number of calls roughly doubles.
- $2 \times 2 \times 2 \times 2 = 16$ - Approximately $2^n=2^4=16$ operations.

#### Example: Generating Subsets
For generating subsequences/ subarrays recursive problem, the caculation is the same.
- At each step need to decide if we want to include/exclude the chosen value - create 2 new function calls.
- If $n$ number of elements in list or string, that would create approximately $2^n$ branches.

---
#### Extention: `O(3ⁿ)`
Sometimes, each recursive call generates 3 new calls instead of 2. Consider the following scenario:

  _You are given a list of numbers (`m`) representing money, where each number is a bill or coin. 
Determine whether it is possible to divide the money into two groups so that both groups 
have the same total amount._

When using recursion to solve this problem, for each bill you can decide to make one of 3 choices: 
- give it to first group (`g1`)
- give it to second group (`g2`)
- give it to neither

```python
func(m=[1,2,3],g1=0,g2=0)
          ├── func(m=[2,3],g1=1,g2=0)
          │              ├── func(m=[3],g1=3,g2=0)
          │              │              ├── func(m=[],g1=6,g2=0)
          │              │              ├── func(m=[],g1=3,g2=3)
          │              │              └── func(m=[],g1=3,g2=0)
          │              ├── func(m=[3],g1=1,g2=2)
          │              │              ├── func(m=[],g1=4,g2=2)
          │              │              ├── func(m=[],g1=1,g2=5)
          │              │              └── func(m=[],g1=3,g2=2)
          │              └── func(m=[3],g1=1,g2=0)
          │                             ├── func(m=[],g1=4,g2=0)
          │                             ├── func(m=[],g1=1,g2=3)
          │                             └── func(m=[],g1=1,g2=0)
          ├── func(m=[2,3],g1=0,g2=1)
          │              ├── func(m=[3],g1=2,g2=1)
          │              │              ├── func(m=[],g1=5,g2=1)
          │              │              ├── func(m=[],g1=2,g2=4)
          │              │              └── func(m=[],g1=2,g2=1)
          │              ├── func(m=[3],g1=0,g2=3)
          │              │              ├── func(m=[],g1=3,g2=3)
          │              │              ├── func(m=[],g1=0,g2=6)
          │              │              └── func(m=[],g1=0,g2=3)
          │              └── func(m=[3],g1=0,g2=1)
          │                            ├── func(m=[],g1=3,g2=1)
          │                            ├── func(m=[],g1=0,g2=4)
          │                            └── func(m=[],g1=0,g2=1)
          └── func(m=[2,3],g1=0,g2=0)
                         ├── func(m=[3],g1=2,g2=0)
                         │             ├── func(m=[],g1=5,g2=0)
                         │             ├── func(m=[],g1=2,g2=3)
                         │             └── func(m=[],g1=2,g2=0)
                         ├── func(m=[3],g1=0,g2=2)
                         │             ├── func(m=[],g1=3,g2=2)
                         │             ├── func(m=[],g1=0,g2=5)
                         │             └── func(m=[],g1=0,g2=2)
                         └── func(m=[3],g1=0,g2=0)
                                       ├── func(m=[],g1=3,g2=0)
                                       ├── func(m=[],g1=0,g2=3)
                                       └── func(m=[],g1=0,g2=0)
```
- Each level branches into 3 new calls
- The recursion depth is still about n
- Total Operations: $3 \times 3 \times 3 \times ... (n \text{ times})=3^n$.

> Exponential complexity occurs when the number of recursive calls grows multiplicatively at each level.
> - $2$ choices per step $\rightarrow O(2^n)$
> - $3$ choices per step $\rightarrow O(3^n)$
> - $k$ choices per step $\rightarrow O(k^n)$

Even small increases in branching lead to huge growth, which is why exponential algorithms become impractical very quickly.

---

<br>

### 6. Factorial Time — $O(n!)$
Very fast growth — even worse than exponential.

#### Example: GeneratingPermutations
_Generate all possible permutation of the string `ABC`._
We build the result step by step:
- Start with an empty string, `c = ""`.
- Decide which letter to place in a specific position at each level.
  - Level 1: First position $\rightarrow$ 3 ($n$) choices (`A`, `B`, `C`),
  - Level 2: Second position $\rightarrow$ 2 ($n-1$) choices for each (remaining letters),
  - Level 3: Third position $\rightarrow$ 1 ($n-2$) choice.

```python
perm(s="ABC",c="")
          ├── perm(s="BC",c="A")
          │              ├── perm(s="C",c="AB")
          │              │              └── perm(s="",c="ABC")
          │              └── perm(s="B",c="AC")
          │                             └── perm(s="",c="ACB")
          ├── perm(s="AC",c="B")
          │              ├── perm(s="C",c="BA")
          │              │              └── perm(s="",c="BAC")
          │              └── perm(s="A",c="BC")
          │                             └── perm(s="",c="BCA")
          └── perm(s="AB",c="C")
                         ├── perm(s="B",c="CA")
                         │              └── perm(s="",c="CAB")
                         └── perm(s="A",c="CB")
                                        └── perm(s="",c="CBA")
```
- Total Operations: $3 \times 2 \times 1 = 3!$
- General case: $n \times (n-1) \times (n-2) \times .... 1 = n!$ 

Factorial growth becomes impractical very quickly:

- $5!$ = 120
- $10!$ = 3,628,800
- $15! \approx$ 1.3 trillion

Even small increases in $n$ lead to massive increases in work.
