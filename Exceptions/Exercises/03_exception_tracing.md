# Exception Tracing: 03 Exercise

> Credit: Erin Carrier
> 
```
def foo(lst):
    try:
        lst.append(4)
        print("entering try")
        x = ord(lst[0][0])/0
        print("leaving try")

    except ZeroDivisionError:
        print("caught zde")
        raise ArithmeticError('was divide by 0')

    except ArithmeticError:
        print("caught ae")
        raise Exception("was an AE")

    except Exception:
        print("caught e")

    else:
        print("no e")
    finally:
        print("finally")

my_lst = ['dog','cat','elephant']

try:
    foo(my_lst)
except ZeroDivisionError:
    print("cannot divide by 0")
except ArithmeticError:
    print("cannot do bad math")
except Exception:
    print("something bad happened")

print(len(my_lst))
```

__Task:__ 
1. Without running the code, trace the flow of execution and determine exactly five lines of output that this program prints. Write them down in the correct order.
2. Suppose the `finally` block is removed and that portion of the code is modified as follows:
   ```
   else:
        print("no e")
    print("finally")
   ```
   How does this change affect the behavior of the program?
3. Given the new output of Q2, describe a practical scenario where having a `finally` block in such nested exception handling would be useful.
   __Hint:__ If you open a file you definitely need to close it.

