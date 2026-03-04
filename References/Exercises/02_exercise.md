## Exercise: Balloon
```python
class Balloon:
    def __init__(self, c):
        self.color = c

b1 = Balloon("purple")
b2 = Balloon("orange")
b3 = Balloon("lime")

b3 = b2
b2.color = "black"
b3.color = "green"
b1.color = "cyan"

print("b1 ", b1.color)
print("b2 ", b2.color)
print("b3 ", b3.color)
print()

def mystery(first, second):
    b = first
    temp = b.color
    first.color = second.color
    second = b
    second.color = temp

b1 = Balloon("purple")
b2 = Balloon("orange")

mystery(b1, b2)

print("b1 ", b1.color)
print("b2 ", b2.color)
print()

def mix_color(first, second):
    b = Balloon("white")
    b = first
    b.color = "blue"
    second.color = first.color
    second = b
    b.color = "yellow"
    first.color = "teal"
    return b

b4 = mix_color(b1, b2)

print("b1 ", b1.color)
print("b2 ", b2.color)
print("b4 ", b4.color)

b4.color = "pink"

print("b1 ", b1.color)
print("b2 ", b2.color)
print("b4 ", b4.color)
```
