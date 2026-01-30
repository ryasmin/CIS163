## **Class Attribute**
Variables that are shared among all instances of a class. They are defined 
- *inside* the class, but
- *outside* of any methods.

Because they belong to the class itself, they do not require `self` to be accessed.

---

### **When should you use class attributes?**
- The value is the same for every object, or
- You want to track information across all instances of a class.

---

### **Example:** `Student` Class

In the following `Student` class, we define two class attributes:

1. `course_num`: Since all students are enrolled in the same course (CIS 163), this value is shared across all instances.

2. `total_students`: This variable keeps track of how many `Student` objects have been created.

```
class Student:
    # === Class Attributes ====
    course_num = '163'        # NO self needed
    total_students = 0        # NO self needed

    # Constructor
    def __init__(self, n, gpa, year):
        # === Instance Attributes ===
        self.name = n
        self.year = year
        self.gpa = gpa

        # Every time a new object is created increase count by 1
        Student.total_students += 1          # Can use both self or Class Name (prefer the latter)

    # === Instance Method ===
    def print_info(self):
      # Note the difference between calling course_num and name/year/gpa
      print(f"{self.name} is a {self.year} with a gpa of {self.gpa} taking CIS{Student.course_num}")   
```

</br>

**Creating Objects (Instances)**
```
# Instantiation of object 1
std1 = Student("Jimmy", 3.7, 'freshman')
std1.print_info()

# Instantiation of object 2
std2 = Student("John", 4.0, 'junior')
std2.print_info()
```

</br>

**Accessing a Class Attribute**
```
# Display total objects created
print(f"Registered Students: {Student.total_students}")
```

---

### Class vs. Instance Attributes

| Feature                     | Class Attribute                   | Instance Attribute |
| --------------------------- | --------------------------------- | ------------------ |
| Belongs to                  | The class itself                  | A specific object  |
| Shared across objects?      | ✅ Yes                             | ❌ No               |
| Defined where?              | Inside the class, outside methods | Inside any method  |
| Accessed using              | `ClassName.attribute`             | `self.attribute`   |
| Requires `self`?            | ❌ No                              | ✅ Yes              |
| Example                     | `Student.course_num`              | `self.name`        |
| Same value for all objects? | ✅ Yes                             | ❌ No               |
