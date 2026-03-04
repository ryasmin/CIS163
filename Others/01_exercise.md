## Exercise: Fix the Method Types
You are given a BankAccount class.

Some methods are incorrectly defined as instance methods, static methods, or class methods.

Your task is to:
- Identify which methods are incorrectly defined.
- Modify each method to use the correct decorator.

```python
class BankAccount:

    bank_name = "Global Bank"
    interest_rate = 0.03

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    # [1]
    def get_bank_name(self):
        return self.bank_name

    # [2]
    def calculate_interest(amount):
        return amount * BankAccount.interest_rate

    # [3]
    def from_string(account_str):
        owner, balance = account_str.split(',')
        return BankAccount(owner, float(balance))

    # [4]
    def deposit(self, amount):
        self.balance += amount

    # [5]
    def set_interest_rate(new_rate):
        BankAccount.interest_rate = new_rate

    # [6]
    def is_valid_amount(amount):
        return amount > 0
```
