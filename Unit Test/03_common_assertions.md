## Common `unittest` Assertions

| Assertion | Purpose | Example |
|----------|---------|---------|
| `assertEqual(a, b)` | Checks that two values are equal | `def add(a, b): return a + b`<br> `self.assertEqual(add(2, 3), 5)` |
| `assertNotEqual(a, b)` | Checks that two values are not equal | `def add(a, b): return a + b`<br> `self.assertNotEqual(add(2, 3), 6)` |
| `assertTrue(x)` | Checks that the expression is `True` | `def is_valid(mystring): return True`<br> `self.assertTrue(is_valid("Secure123"))` |
| `assertFalse(x)` | Checks that the expression is `False` | `def not_valid(mystring): return False`<br> `self.assertFalse(not_valid("NotSecure"))` |
| `assertIs(a, b)` | Checks that two variables reference the **same object** | `obj1 = "Hello"`<br> `obj2 = obj1`<br> `self.assertIs(obj1, obj2)` |
| `assertIsNot(a, b)` | Checks that two variables reference **different objects** | `obj1 = "Hello"`<br> `obj2 = "Hi"`<br> `self.assertIsNot(obj1, obj2)` |
| `assertIsNone(x)` | Checks that a value is `None` | `self.assertIsNone(find_user("unknown"))` |
| `assertIsNotNone(x)` | Checks that a value is not `None` | `user = "Student"`<br> `self.assertIsNotNone(user)` |
| `assertIn(a, b)` | Checks that `a` is contained in `b` | `user_roles = ["Admin", "User"]`<br> `self.assertIn("Admin", user_roles)` |
| `assertNotIn(a, b)` | Checks that `a` is not contained in `b` | `user_roles = ["Admin", "User"]`<br> `self.assertNotIn("Guest", user_roles)` |
| `assertAlmostEqual(a, b, places=2)` | Checks that two numbers are approximately equal (useful for floats) | `total = 0.1 + 0.2` <br>`self.assertAlmostEqual(total, 0.3)` |
| `assertRaises(Exception)` | Checks that a function raises a specific exception | `with self.assertRaises(Exception):`<br> `  divide(5, 0)` |
| `assertGreater(a, b)` | Checks that `a > b` | `self.assertGreater(score, 50)` |
| `assertLess(a, b)` | Checks that `a < b` | `self.assertLess(error_rate, 0.1)` |
