# Exception Tracing: Exercise 02

```
def register_ticket():
    name = input("Enter your name: ")
    age_str = input("Enter your age: ")
    tickets_str = input("How many tickets do you want? ")

    print("Step 1: Raw inputs collected.")

    # Built-in ValueError possible here
    age = int(age_str)
    tickets = int(tickets_str)

    print("Step 2: Converted age and tickets to int.")

    if not name.strip():
        raise ValueError("Name cannot be empty.")

    if age <= 0:
        raise ValueError("Age must be positive.")

    if tickets <= 0:
        raise ValueError("You must request at least one ticket.")

    if tickets > 5:
        raise ValueError("You cannot buy more than 5 tickets.")

    print("Step 3: All checks passed.")
    return f"Registration complete for {name}, {tickets} ticket(s)."


try:
    result = register_ticket()
    
except ValueError as e:
    print("Caught ValueError in except block:", e)

else:
    print("No errors occurred.")
    print("Result from function:", result)

finally:
    print("Thank you for using the ticket system.")
```

Consider each of the following scenarios.

| Scenario | Name Input (`name`) | Age Input (`age_str`) | Tickets Input (`tickets_str`) |
| -------- | ------------------- | --------------------- | ----------------------------- |
| A        | `"Alice"`           | `"20"`                | `"2"`                         |
| B        | `""` (empty string) | `"25"`                | `"1"`                         |
| C        | `"Bob"`             | `"-3"`                | `"2"`                         |
| D        | `"Charlie"`         | `"twenty"`            | `"2"`                         |
| E        | `"Dana"`            | `"30"`                | `"8"`                         |

__Tasks:__ For each scenario trace the program carefully and fill out the following table:
| Scenario | Do `int(...)` conversions succeed? | Where does the error occur? (line/check) | Built-in or forced `ValueError`? | Does the `else` block run? | What does the `except` block print? | Does the `finally` block run? |
| -------- | ---------------------------------- | ---------------------------------------- | -------------------------------- | -------------------------- | ----------------------------------- | ----------------------------- |
| A        |                                    |                                          |                                  |                            |                                     |                               |
| B        |                                    |                                          |                                  |                            |                                     |                               |
| C        |                                    |                                          |                                  |                            |                                     |                               |
| D        |                                    |                                          |                                  |                            |                                     |                               |
| E        |                                    |                                          |                                  |                            |                                     |                               |


