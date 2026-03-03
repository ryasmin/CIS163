## Exercise: Widget

```
class Widget:
    def __init__(self, name, value):
        self.name = name
        self.value = value

    def bump(self, amount):
        self.value += amount

    def rename(self, new):
        self.name = new

    def __add__(self, other):
        self.value += other.value
        return self

def scramble(a, b):
    x = a
    y = Widget("temp", 0)
    y = b
    x.bump(5)
    b = Widget("fresh", 100)
    y.rename("Y")
    return x

def mix(u, v, w):
    z = u + v
    w = z
    z.rename("Z")
    v.bump(10)
    return w

w1 = Widget("A", 10)
w2 = Widget("B", 20)
w3 = Widget("C", 30)

w4 = scramble(w1, w2)
w5 = mix(w4, w2, w3)

w5.bump(3)
w2.rename("B2")

print("w1:", w1.name, w1.value)
print("w2:", w2.name, w2.value)
print("w3:", w3.name, w3.value)
print("w4:", w4.name, w4.value)
print("w5:", w5.name, w5.value)
```
