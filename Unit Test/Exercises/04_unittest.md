## Unittest Exercise

Write all necessary unuttest using the `unittest` module for the following class:

```python
class BankAccount:
    def __init__(self, owner, balance=0.0):
        if not isinstance(owner, str) or owner.strip() == "":
            raise ValueError("Owner name must be a non-empty string.")
        
        if balance < 0:
            raise ValueError("Initial balance cannot be negative.")
        
        self.owner = owner
        self.balance = float(balance)

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive.")
        
        self.balance += amount
        return self.balance

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive.")
        
        if amount > self.balance:
            raise ValueError("Insufficient funds.")
        
        self.balance -= amount
        return self.balance

    def transfer(self, other_account, amount):
        if not isinstance(other_account, BankAccount):
            raise TypeError("Transfer requires another BankAccount.")
        
        self.withdraw(amount)
        other_account.deposit(amount)
        return self.balance

    def __eq__(self, other):
        if not isinstance(other, BankAccount):
            return False
        return self.owner == other.owner and self.balance == other.balance
```

<details>
  <summary> Solution (Click to expand)</summary>
  
```python
import unittest
from bank_account import BankAccount

class TestBankAccount(unittest.TestCase):
  
      def setUp(self):
          self.acc1 = BankAccount("Alice", 100.0)
  
      # Test Constructor are correct
      def test_valid_account_creation(self):
          self.assertEqual(self.acc1.owner, "Alice")
          self.assertEqual(self.acc1.balance, 100.0)

      # Test Constructor: Invalid name
      def test_invalid_owner(self):
          with self.assertRaises(ValueError):
              acc = BankAccount("", 100)

      # Test Constructor: Invalid balance
      def test_negative_initial_balance(self):
          with self.assertRaises(ValueError):
              acc = BankAccount("Alice", -10)
  

      # Test Deposit
      def test_deposit_valid(self):
          test_cases = [
            (50, 150.0),
            (25.5, 125.5),
            (0.1, 100.1),]

          for amount, expected in test_cases:
              with self.subTest(amount=amount):
                  acc = BankAccount("Test", 100.0)
                  acc.deposit(amount)
                  self.assertAlmostEqual(acc.balance, expected, places=2)
  
      def test_deposit_invalid(self):
          with self.assertRaises(ValueError):
              self.acc1.deposit(-10)
  
      # Test Withdraw
      def test_withdraw_valid(self):
          new_balance = self.acc1.withdraw(40)
          self.assertEqual(new_balance, 60.0)
  
      def test_withdraw_invalid(self):
          invalid_cases = [0, -5, 200]

          for amount in invalid_cases:
              with self.subTest(amount=amount):
                  with self.assertRaises(ValueError):
                      self.acc1.withdraw(amount)
  
      # Test Transfer
      def test_transfer_valid(self):
          acc2 = BankAccount("Bob", 50.0)
          self.acc1.transfer(acc2, 30)
          self.assertEqual(self.acc1.balance, 70.0)
          self.assertEqual(acc2.balance, 80.0)
  
      def test_transfer_invalid_account(self):
          with self.assertRaises(TypeError):
              self.acc1.transfer("not_account", 10)
  
      def test_transfer_insufficient_funds(self):
          acc2 = BankAccount("Bob", 50.0)
          with self.assertRaises(ValueError):
              self.acc1.transfer(acc2, 1000)
  
      # Tests Equality
      def test_account_equality(self):
          cases = [
            (self.acc1, BankAccount("Alice", 100.0), True),
            (self.acc1, BankAccount("Alice", 90.0), False),
            (self.acc1, 100, False),]

          for acc_a, acc_b, expected in cases:
              with self.subTest(acc_a=acc_a, acc_b=acc_b):
                  self.assertEqual(acc_a == acc_b, expected)
  
if __name__ == "__main__":
    unittest.main()

```
</details>
