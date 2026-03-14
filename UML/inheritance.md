# Inheritance

Inheritance allows one class to reuse code from another class.

It helps us avoid repetition and makes programs easier to maintain.

In Inheritance:
1. __Base/Parent/Super Class__ $\rightarrow$ The class whose attributes and behaviors other classes can reuse.
2. __Derived/Child/Sub Class__ $\rightarrow$ The class that inherits attributes and behaviors from another class.

<br>

## Characteristics

#### 1. IS-A Relationship
Inheritance models an “IS-A” relationship between classes.

   > $$\text{Class A "IS-A" Class B}$$

If this sentence makes sense $\Rightarrow$ then inheritance is appropriate.

Example:
- `Dog` IS-AN `Animal` $\Rightarrow$ ✔️ inheritance makes sense
- `Car` IS-AN `Engine` $\Rightarrow$ ✖️ should probably not be inheritance

#### 2. Use of `super()`
__`super()`__ allows a child class to call methods from its parent class.
  - Reuse parent initialization
  - Extend (NOT replace) parent behavior



    
