## Level: Difficult

#### Exercise 1: Flood Fill Algorithm
You are given a 2D grid (list of lists) of integers, where each number represents a color.

Write a recursive function using a helper that starts from a given cell and changes its color. 
When you change that cell, you must also change all neighboring cells that have the same original color and are connected to it.

```
def flood_fill(image, start_row, start_col, new_color):
  pass

image = [
    [1, 1, 0, 0],
    [1, 1, 1, 0],
    [0, 0, 1, 1],
    [0, 0, 1, 1]]

flood_fill(image, 0, 0, 2)
print(image)

# Expected solution:
   [[2, 2, 0, 0],
    [2, 2, 2, 0],
    [0, 0, 2, 2],
    [0, 0, 2, 2]]
```

#### Exercise 2: Count the Size of an Island
You are given a 2D grid of '0's and '1's, where:
- '1' represents land '0' represents water

Write a recursive function using a helper that returns the size of the largest connected island in the grid. 
An island is formed by connecting adjacent lands vertically or horizontally (not diagonally).
```
def largest_island(grid):
  pass

print(largest_island(grid))  # Expected Output: 4
```

