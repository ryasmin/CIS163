# Overview of OOP Principle
The Four Pillars of OOP
1. Encapsulation: 
    - Protect and Control access to internal data
    - Avoid accidental modifications
2. Abstraction: 
    - Hiding Unnecessary implementation details
    - Creating Consistent and structured framework
3. Inheritance
    - Reusability and extension of another class
4. Polymorphism
    - Interchangeable code
    - Create flexible and scalable design

<br>

---

# Polymorphism Basics
> Poly - > many, Morph -> form

__Definition:__ Use the same method (function) name on (with) different objects (parameters) and depending on the object (parameters), it will do different things

## Four different ways to achieve Polymorphism in Python
### 1. Duck Typing
  ```
  Dog: speak() -> “woof”
  Cat: speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Dog())
  myfunc(Cat())
  ```
### 2. Interface
  ```
  Animal:      speak(): @abtractmethod 
  Dog(Animal): speak() -> “woof”
  Cat(Animal): speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Dog())
  myfunc(Cat())
  ```

### 3. Inheritance/ Method Overriding
  ```
  Animal:      speak() -> “generic sound”
  Dog(Animal): speak() -> “woof”
  Cat(Animal): speak() -> “meow”

  def myfunc(obj): print(obj.speak())

  myfunc(Animal())
  myfunc(Dog())
  myfunc(Cat())
  ```

### 4. Operator Overloading

<br>

## Why Polymorphism is important:
1. Otherwise creates long chain of conditionals
    ```
  	if isinstance(obj, Dog):
  		obj.dog_speak()
  	if isinstance(obj, Cat):
  		obj.cat_speak()
    ...
    ```
2. Maintenance issue
    - If another class say `Pig` needs to be added, you will need to go in and change the if-else conditions.
    - Easily breaks code if not careful.

<br>

## Method Signature
A method signature describes:
1. The method name
2. The parameters

> For polymorphism to work properly, method signatures must be compatible.
```
RobotDog: speak(volume) -> “beep at {volume}”
```

- __Problem:__ If we pass `RobotDog` to `myfunc` we get a `TypeError`.

- __Why?__ Because the method signatures are different, even though both classes have a method named speak, they are not polymorphically compatible.

- __Solution:__ Make every `speak` method accept the same parameters.
  ```
  Dog:      speak(volume=None) -> “woof”
  Cat:      speak(volume=None) -> “meow”
  RobotDog: speak(volume)      -> “beep at {volume}”
  ```

- __Takeaway:__ Polymorphism is not just “same method name.” It is:
  - Same method name
  - Compatible method signature (parameters + types)
