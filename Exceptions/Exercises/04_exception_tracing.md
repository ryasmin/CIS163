# Exception Tracing: 03 Exercise

> Credit: Erin Carrier
> 
```
class ExceptionFun:
  
    def __init__(self, n):
        self.mylst = []
        for i in range(n):
            self.mylst = None

    def mixup(self):
        for i in range(1, len(self.mylst)+1):
            self.mylst[i].repaint(i)

class Car:
    def __init__(self):
        self.color = 'blue'
        self.doors = 4

    def repaint(self, num):
        if num % 3 == 0:
            self.color = 'black'
        elif num % 2 == 0:
            self.color = 'silver'
        else:
            self.color = 'white'


if __name__ == '__main__':
    ef = ExceptionFun(10)

    try:
        print('calling mixup')
        ef.mixup()
        print('done calling mixup')
    except IndexError:
        print('tried to access out of bounds')
    except Exception:
        print('other exception')
    finally:
        print('all finished')
```

__Tasks:__ 

1. Without running the code, trace the flow of execution and determine the output that this program prints. Write them down in the correct order.
2. Suppose the `__init__` method in `ExceptionFun` is modified as follows:
    ```
    def __init__(self, n):
        self.mylst = []
        for i in range(n):
            self.mylst.append(Car())
    ```
    How does this change affect the behavior of the program?
3. What additional changes (if any) are required to ensure the program runs without raising any exceptions?
   
