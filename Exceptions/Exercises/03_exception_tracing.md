# Exception Tracing: 03 Exercise

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
        print('caught ae')
        raise Exception('was an AE')
    except Exception:
        print("caught e")
    else:
        print('no e')
    finally:
        print("finally")

my_lst = ['dog','cat','elephant']
try:
    foo(my_lst)
except ZeroDivisionError:
    print('cannot divide by 0')
except ArithmeticError:
    print('cannot do bad math')
except Exception:
    print('something bad happened')
print(len(my_lst))
```

__Task:__ Running this program will give exactly 5 lines of output. What will they be?
