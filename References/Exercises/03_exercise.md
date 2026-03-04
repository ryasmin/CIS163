## Exercise: Car
```python
class Car:

    def __init__(self, color, doors):
        self.color = color
        self.doors = doors

    def change_doors(self, d):
        self.doors = d

    def repaint(self, c):
        self.color = c

    def crash(self, c2, c3):
        c4 = c3
        c5 = Car("orange", 2)
        c3 = c5
        self.repaint(c2.color)
        self.doors -= 1
        c4.change_doors(c4.doors - 2)
        c2 = self
        c3.repaint(self.color)
        c5.repaint("blue")
        c2 = c5

c1 = Car("black", 4)
c2 = Car("yellow", 3)
c3 = Car("green", 2)

c3.crash(c1, c2)

# Part A
print(c1.color, c1.doors)
print(c2.color, c2.doors)
print(c3.color, c3.doors)

c4 = Car("black", 4)
c5 = Car("green", 2)

c4.crash(c5, c5)

# Part B
print(c4.color, c4.doors)
print(c5.color, c5.doors)
```
