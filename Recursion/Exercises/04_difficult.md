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

<details>
  <summary> Solution (Without Helper) - Click to expand!</summary>
  
  ```python
  def flood_fill(image, sr, sc, new_color, original_color=None):
    rows, cols = len(image), len(image[0])

    if original_color == None:
      original_color = image[sr][sc]

    if sr < 0 or sr >= rows or sc < 0 or sc >= cols or image[sr][sc] != original_color or image[sr][sc] == new_color:
        return

    image[sr][sc] = new_color

    flood_fill(image, sr - 1, sc, new_color, original_color)  # Up
    flood_fill(image, sr + 1, sc, new_color, original_color)  # Down
    flood_fill(image, sr, sc - 1, new_color, original_color)  # Left
    flood_fill(image, sr, sc + 1, new_color, original_color)  # Right
  ```
#### Explanation
- We must store the original color so that only cells matching the starting color are replaced.
- Using `original_color == None` ensures the value is initialized only once (on the first call).
  Without this, `original_color` could be overwritten during recursion by another color.
- Boundary Conditions: STOP if the indices go outside the grid
  - `sr < 0 or sr >= rows or sc < 0 or sc >= cols`.
- Only want to color the connected cells whose color matches `original_color`,
  - If the cell color does not match `original_color` -> STOP: `image[sr][sc] != original_color`.
- If cell is already visited -> STOP: `image[sr][sc] == new_color`.
</details>

<br>

<details>
  <summary>Solution (With Helper) - Click to expand!</summary>

  ```python
  def flood_fill(image, sr, sc, new_color):
    rows, cols = len(image), len(image[0])

    original_color = image[sr][sc]

    def helper(sr, sc):

      if sr < 0 or sr >= rows or sc < 0 or sc >= cols or image[sr][sc] != original_color or image[sr][sc] == new_color:
          return

      image[sr][sc] = new_color

      helper(sr - 1, sc)  # Up
      helper(sr + 1, sc)  # Down
      helper(sr, sc - 1)  # Left
      helper(sr, sc + 1)  # Right

    helper(sr, sc)
  ```

</details>

<br>

#### Exercise 2: Count the Size of an Island
You are given a 2D grid of '0's and '1's, where:
- '1' represents land '0' represents water

Write a recursive function using a helper that returns the size of the largest connected island in the grid. 
An island is formed by connecting adjacent lands vertically or horizontally (not diagonally).
```
def largest_island(grid):
  pass

grid = [
    ['1','1','0','0'],
    ['1','0','0','1'],
    ['0','0','1','1'],
    ['0','0','0','1']
]
print(largest_island(grid))  # Expected Output: 4
```

<details>
  <summary> Solution - Click to expand!</summary>
  
  ```python
  def largest_island(grid):
    rows, cols = len(grid), len(grid[0])

    def helper(sr, sc):
        if sr < 0 or sr >= rows or sc < 0 or sc >= cols or grid[sr][sc] != '1':
            return 0

        grid[sr][sc] = '0'

        return 1 + helper(sr+1, sc) + helper(sr-1, sc) + helper(sr, sc+1) + helper(sr, sc-1)

    island_size = []

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                size = helper(r, c)
                island_size.append(size)

    return max(island_size)
  ```
</details>
