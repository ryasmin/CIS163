## What is a Debugger?

A debugger lets you:
- Pause execution
- Inspect variables
- Step through code slowly

<br>

## Setup in VS Code

#### Step 1: Install Python Extension
- Open VS Code
- Go to Extensions 
- Install: Python Debugger (by Microsoft)

#### Step 2: Create a Python File
Use the following code and name the file `starwars_students.py`.

```python
class Student:
    def __init__(self, name, midterm, final):
        self.name = name
        self.midterm = midterm
        self.final = final

    def calculate_score(self):
        return (self.midterm * 0.4) + (self.final * 0.6)

    def get_grade(self):
        score = self.calculate_score()
        
        if score >= 90:
            return "A"
        elif score >= 80:
            return "B"
        elif score >= 70:
            return "C"
        else:
            return "F"

def main():
    students = [
        Student("Luke", 85, 95),
        Student("Anakin", 95, 40), 
        Student("Rey", 88, 92)]

    for s in students:
        score = s.calculate_score()
        grade = s.get_grade()
        print(f"{s.name}: Score={score}, Grade={grade}")

if __name__ == "__main__":
    main()
```

<br>

## Using the Debugger
#### Set a Breakpoint
A breakpoint is a marker you place in your code that tells the program:
> “Pause execution here so I can inspect what’s happening.”

