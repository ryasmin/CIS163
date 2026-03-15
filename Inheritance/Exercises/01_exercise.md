## Code Tracing Exercises

### Exercise 1
```python
class Parent:
    def show(self):
        print("Parent's show() method")

class Child(Parent):
    def show(self):
        print("Child's show() method")

obj = Child()
obj.show()
```

<br>

### Exercise 2
```python
class A:
    def display(self):
        print("Class A display()")

class B(A):
    def display(self):
        super().display()
        print("Class B display()")

obj = B()
obj.display()
```

<br>

### Exercise 3
```python
class Grandparent:
    def greet(self):
        print("Hello from Grandparent")

class Parent(Grandparent):
    def greet(self):
        print("Hello from Parent")

class Child(Parent):
    pass

obj = Child()
obj.greet()
```

<br>

### Exercise 4
```python
class SomeOne:
    def msg(self):
        return "Hello"
    
    def show(self):
        print(self.msg())

class NoOne(SomeOne):
    def msg(self):
        return "Hi"

c = NoOne()
c.show()
```

<br>

### Exercise 5
```python
class Animal:
    def __init__(self, species):
        print(f"Animal created: {species}")

class Dog(Animal):
    def __init__(self, breed):
        super().__init__("Dog")
        print(f"Dog breed: {breed}")

dog = Dog("Golden Retriever")
```

<br>

### Exercise 6
```python
class Animal:
    def __init__(self, species):
        print(f"Animal created: {species}")

class Mammal(Animal):
    def __init__(self, species, is_warm_blooded):
        super().__init__(species)
        print(f"Warm-blooded: {is_warm_blooded}")

class Dog(Mammal):
    def __init__(self, breed):
        super().__init__("Dog", True)
        print(f"Dog breed: {breed}")

dog = Dog("Labrador")
```

<br>

### Exercise 7
```python
class Employee:
    def __init__(self, name, emp_id):
        self.name = name
        self.emp_id = emp_id
        print(f"Employee Created: {self.name} (ID: {self.emp_id})")

    def get_details(self):
        return f"Employee: {self.name}, ID: {self.emp_id}"

class FullTimeEmployee(Employee):
    def __init__(self, name, emp_id, salary, benefits):
        super().__init__(name, emp_id)
        self.salary = salary
        self.benefits = benefits
        print(f"Full-Time Employee: {self.name}, Salary: ${self.salary}")

class ContractEmployee(Employee):
    def __init__(self, name, emp_id, hourly_rate):
        super().__init__(name, emp_id)
        self.hourly_rate = hourly_rate
        print(f"Contract Employee: {self.name}, Hourly Rate: ${self.hourly_rate}/hr")

class Manager(FullTimeEmployee):
    def __init__(self, name, emp_id, salary, benefits, bonus):
        super().__init__(name, emp_id, salary, benefits)
        self.bonus = bonus
        print(f"Manager: {self.name}, Bonus: ${self.bonus}")

    def approve_leave(self, days):
        print(f"Manager {self.name} approved {days} days of leave.")

# Creating instances
e1 = FullTimeEmployee("Alice", 101, 70000, ["Health Insurance", "401k"])
e2 = ContractEmployee("Bob", 202, 50)
e3 = Manager("Charlie", 303, 90000, ["Stock Options", "401k"], 10000)

e3.approve_leave(5)
```

<br>

### Exercise 8
```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price
        print(f"Product Created: {self.name} - ${self.price}")

class Shippable:
    def __init__(self, weight, shipping_cost):
        self.weight = weight
        self.shipping_cost = shipping_cost
        print(f"Shippable: Weight {self.weight}kg, Shipping Cost: ${self.shipping_cost}")

class Downloadable:
    def __init__(self, file_size):
        self.file_size = file_size
        print(f"Downloadable: File Size {self.file_size}MB")

class Ebook(Product, Shippable, Downloadable):
    def __init__(self, name, price, weight, shipping_cost, file_size):
        Product.__init__(self, name, price)
        Shippable.__init__(self, weight, shipping_cost)
        Downloadable.__init__(self, file_size)
        print(f"Ebook Created: {self.name}")

ebook1 = Ebook("Python Mastery", 30, 0.5, 5, 20)
```

<br>

### Exercise 9
```python
class Animal:
    kingdom = "Animalia"
    total_animals = 0

    def __init__(self, name, age, sound):
        self.name = name
        self.age = age
        self.sound = sound
        Animal.total_animals += 1
        print(f"Animal created: {self.name}")

    def make_sound(self):
        print(f"{self.name} says: {self.sound}")

    def birthday(self):
        self.age += 1
        print(f"{self.name} is now {self.age} years old.")

    def info(self):
        return f"{self.name} is {self.age} years old."


class Mammal(Animal):
    def __init__(self, name, age, sound, fur_color, number_of_legs):
        super().__init__(name, age, sound)
        self.fur_color = fur_color
        self.number_of_legs = number_of_legs
        print(f"{self.name} is a mammal with {self.fur_color} fur.")

    def make_sound(self):
        print(f"Mammal sound check for {self.name}")
        super().make_sound()

    def give_birth(self, baby_name):
        print(f"{self.name} gave birth to {baby_name}")
        return Mammal(
            baby_name,
            0,
            self.sound,
            self.fur_color,
            self.number_of_legs
        )

    def move(self):
        print(f"{self.name} walks on {self.number_of_legs} legs.")


class Bird(Animal):
    def __init__(self, name, age, sound, wingspan):
        super().__init__(name, age, sound)
        self.wingspan = wingspan
        print(f"{self.name} is a bird with a wingspan of {self.wingspan}.")

    def move(self):
        print(f"{self.name} flies through the sky.")

    def birthday(self):
        print(f"Checking birthday for bird {self.name}")
        super().birthday()


class Reptile(Animal):
    def __init__(self, name, age, sound, scale_color):
        super().__init__(name, age, sound)
        self.scale_color = scale_color
        print(f"{self.name} is a reptile with {self.scale_color} scales.")

    def move(self):
        print(f"{self.name} crawls slowly.")

    def shed_skin(self):
        print(f"{self.name} shed its {self.scale_color} skin.")


class Dog(Mammal):
    species = "Dog"

    def __init__(self, name, age, fur_color):
        super().__init__(name, age, "Woof", fur_color, 4)
        print(f"{self.name} is specifically a dog.")

    def fetch(self, item):
        print(f"{self.name} fetches the {item}.")


class Eagle(Bird):
    species = "Eagle"

    def __init__(self, name, age):
        super().__init__(name, age, "Screech", "Large")

    def make_sound(self):
        print(f"{self.name} the eagle prepares to make a sound.")
        super().make_sound()


dog = Dog("Molly", 5, "Brown")
eagle = Eagle("Sky", 3)
turtle = Reptile("Shelly", 10, "Hiss", "Green")

dog.make_sound()
dog.move()
dog.fetch("ball")
print()

baby_dog = dog.give_birth("Charlie")
baby_dog.make_sound()
baby_dog.birthday()
print()

eagle.make_sound()
eagle.move()
eagle.birthday()
print()

turtle.make_sound()
turtle.move()
turtle.shed_skin()
print()

print(dog.info())
print(baby_dog.info())
print(eagle.info())
print(turtle.info())
print()

print(Animal.kingdom)
print(Animal.total_animals)
print(Dog.species)
print(Eagle.species)
```

<br>

### Exercise 10
```python
class BankAccount:
    bank_name = "Global Bank"
    interest_rate = 0.02

    def __init__(self, acc_holder, balance):
        self.acc_holder = acc_holder
        self.balance = balance
        print(f"Account Created: {self.acc_holder}, Balance: ${self.balance}")

class CheckingAccount(BankAccount):
    interest_rate = 0.01

class SavingsAccount(BankAccount):
    def __init__(self, acc_holder, balance, interest_rate=None):
        super().__init__(acc_holder, balance)
        if interest_rate:
            self.interest_rate = interest_rate
        print(f"Savings Account: Interest Rate: {self.interest_rate}")

acc1 = CheckingAccount("Alice", 5000)
acc2 = SavingsAccount("Bob", 10000, 0.03)

print(acc1.bank_name, acc1.interest_rate)
print(acc2.bank_name, acc2.interest_rate)
```
