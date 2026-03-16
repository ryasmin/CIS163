## Unittest Exercise
Write unit tests for the function below using Python’s `unittest` module.
```python
def validate_password(password):
    """
    Validates a password based on several rules.

    Rules:
    - Must be a string
    - Must be at least 8 characters long
    - Must contain at least one digit
    - Must contain at least one uppercase letter
    """

    if not isinstance(password, str):
        raise TypeError("Password must be a string.")

    if len(password) < 8:
        raise ValueError("Password must be at least 8 characters long.")

    if not any(char.isdigit() for char in password):
        raise ValueError("Password must contain at least one digit.")

    if not any(char.isupper() for char in password):
        raise ValueError("Password must contain at least one uppercase letter.")

    return True
```

