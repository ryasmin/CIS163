### Algorithmic Complexity Practice
For each function:
- Count how many times the loop executes
- Determine the Big-O complexity

#### Set 1
```python
def foo(n):
    i = n
    while i >= 1:
        i -= 2
```
__Description:__ The loop decreases $i$ by a constant amount each time.

<details> <summary>Answer</summary>

- Initial value: $i = n$
- Each iteration: subtract $2 \rightarrow i = n, n-2, n-4, ...$
- The loop stops when $i \le 1$
- So the loop runs about: $n/2$ times
- Example: if $n=6$, $i = 6, 4, 2, 0$ $\rightarrow$ about $n/2$ iterations.

Total Iterations $\approx n/2$; Time Complexity: $O(n)$

</details>

```python
def foo(n):
    i = 1
    while i < n:
        i += 2
```
__Description:__ The loop increases $i$ by a constant amount each time.

<details> <summary>Answer</summary>

- Initial value: $i = 1$
- Each iteration: add $2 \rightarrow i = 1, 3, 5, 7, ...$
- The loop stops when $i \ge n$
- So the loop runs about: $n/2$ times
- Example: if $n=7$, $i = 1,3,5,7$ $\rightarrow$ about $n/2$ iterations

Total Iterations $\approx n/2$; Time Complexity: $O(n)$

</details>

<br>

#### Set 2

```python
def foo(n):
    i = n
    while i > 1:
        i = i // 2
```
__Description:__ The loop repeatedly halves $i$.

<details> <summary>Answer</summary>

- Initial value: $i = n$
- Each iteration: divide by $2 \rightarrow n, n/2, n/4, n/8, ...$
- The loop stops when $i \leq 1$
- So the loop runs about: $\log_2 n$ times
- Example: if $n=16$, $i = 16,8,4,2,1$ $\rightarrow$ about $\log_2 16 = 4$ iterations

Total Iterations $\approx \log n$; Time Complexity: $O(\log n)$

</details>

```python
def foo(n):
    i = 1
    while i < n:
        i *= 2
```
__Description:__ The loop doubles $i$ each time.

<details> <summary>Answer</summary>

- Initial value: $i = 1$
- Each iteration: $i = 1, 2, 4, 8, ...$
- Stops when $i \ge n$
- So the loop runs about: $\log_2 n$ times
- Example: if $n=16$, $i = 1, 2, 4, 8$ $\rightarrow$ about $\log_2 16 = 4$ iterations

Total Iterations $\approx \log n$; Time Complexity: $O(\log n)$

</details>

```python
def foo(n):
    i = 1
    while i < n:
        i *= 5
```

__Description:__ The loop grows $i$ multiplicatively as a factor of 5.

<details> <summary>Answer</summary>

- Initial value: $i = 1$
- Each iteration: $i = 1, 5, 25, 125, ...$
- Stops when $i \ge n$
- So the loop runs about: $\log_5 n$ times.

Total Iterations $\approx \log_5 n$; Time Complexity: $O(\log_5 n)$

</details>

<br>

#### Set 3

```python
def foo(n):
    for i in range(n):
        for j in range(i + n):
            print(i, j)
```
__Description:__ The inner loop runs slightly more than $n$ times per iteration.

<details> <summary>Answer</summary>

- Outer loop runs $n$ times
- Inner loop runs $n + i$ times for each $i = 0, 1, 2, ...$
- Total work: $(n + 0) + (n + 1) + (n + 2) + .... + (n + (n-1)) = n^2 + n \times (n-1) /2$
- Dominant term is $n^2$

Time Complexity: $O(n^2)$

</details>

```python
def foo(n):
    i = 0
    while i < n:
        j = 0
        while j < n:
            print(i, j)
            j += 1
        i += 1
```
__Description:__ A full nested loop where both loops run up to $n$.

<details> <summary>Answer</summary>

- Outer loop runs $n$ times
- Inner loop runs $n$ times per outer iteration
- Total: $n \times n = n^2$

Total Iterations $\approx n^2$; Time Complexity: $O(n^2)$

</details>

<br>

#### Set 4

```python
def foo(n):
    for i in range(n):
        j = 1
        while j < n:
            j *= 2
```
__Description:__ A linear loop combined with a logarithmic inner loop.

<details> <summary>Answer</summary>

- Outer loop runs $n$ times
- Inner loop doubles each time $\rightarrow$ $\log n$ iterations for each outer loop
- Total work: $n \log n$

Time Complexity: $O(n \log n)$

</details>

```python
def foo(n):
  for i in range(n // 2, n):
      j = 1
      while j < n:
          j = j * 2
```
__Description:__ Outer loop runs half of $n$, with a logarithmic inner loop.

<details> <summary>Answer</summary>

- Outer loop runs $n/2$ times
- Inner loop doubles each time $\rightarrow$ $\log n$ iterations for each outer loop
- Total work: $n/2 \log n$

Time Complexity: $O(n \log n)$

</details>

<br>

#### Set 5

```python
def foo(n):
    i = 1
    while i < n:
        j = 1
        while j < n:
            j *= 2
        i *= 2
```
__Description:__ Two nested logarithmic loops.

<details> <summary>Answer</summary>

- Outer loop runs $\log n$
- Inner loop runs $\log n$ times for each outer loop
- Total work: $\log n \times \log n = (\log n)^2$

Time Complexity: $O(\log^2 n)$

</details>

```python
def foo(n):
    low = 0
    high = n - 1
    while low <= high:
        mid = (low + high) // 2
        high = mid - 1
```
__Description:__ The search space is halved each iteration.

<details> <summary>Answer</summary>

- Each step reduces problem size by half: $n \rightarrow n/2 \rightarrow n/4 \rightarrow ...$
- Stops after $\log n$ steps.

Time Complexity: $O(\log n)$

</details>

```python
def function(n):
    count = 0
    for i in range(n // 2, n + 1):
        j = 1
        while j <= n:
            k = 1
            while k <= n:
                count += 1
                k *= 2
            j *= 2
```
__Description:__ Three nested loops: linear, logarithmic, and logarithmic.

<details> <summary>Answer</summary>

- Outer loop runs $n/2$ 
- Middle loop runs $\log n$
- Inner loop runs $\log n$
- Total: $n/2 \times \log n \log n$

Time Complexity: $O(n \log^2 n)$

</details>

