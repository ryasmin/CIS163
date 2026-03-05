## Part A — The Story: “Potion Shop”
You run a small fantasy potion shop. The shop has:
- gold (money),
- an inventory of potion counts,
- and fixed prices.

Buying a potion changes the shop’s state:
- gold decreases,
- inventory increases,
- and the method returns a receipt string.

```python
class PotionShop:
    def __init__(self, gold=100):
        self.gold = gold
        self.inventory = {"health": 3, "mana": 2}
        self.prices = {"health": 10, "mana": 15}

    def buy(self, kind):
        self.gold -= self.prices[kind]
        self.inventory[kind] += 1
        return f"bought {kind}"

    def count(self, kind):
        return self.inventory.get(kind, 0)
```

## Part B — Testing Class Behavior

When we buy "health":
- `health` count should increase by 1,
- `gold` should decrease by the health price.

```
import unittest

class TestPotionShop(unittest.TestCase):

    def test_buy_health_updates_gold_and_inventory(self):
        shop = PotionShop(100)
        receipt = shop.buy("health")

        self.assertEqual(receipt, "bought health")
        self.assertEqual(shop.count("health"), 4)
        self.assertEqual(shop.gold, 90)
```
__Note:__
- Need to create an instance of the object before we can test it.

__Questions:__
- Why are we checking all three (health, gold, and function return) in the same test?

## Part C — The Most Common Mistake: Shared State Between Tests
This version creates a single shop that all tests share:
```
class TestPotionShopBad(unittest.TestCase):
    shop = PotionShop(100)

    def test_buy_health(self):
        self.shop.buy("health")
        self.assertEqual(self.shop.count("health"), 4)
        self.assertEqual(self.shop.gold, 90)

    def test_buy_mana(self):
        self.shop.buy("mana")
        self.assertEqual(self.shop.count("mana"), 3)
        self.assertEqual(self.shop.gold, 85)
```

__Questions:__
- After both tests run, what are `shop.gold`, `shop.count("health")`, `shop.count("mana")`?
- Which test becomes wrong if order swaps?

#### Why this is a bad design

The tests are now dependent on execution order.
If `test_buy_health` runs before `test_buy_mana`, the `gold` and `inventory` will already have changed.

This leads to “flaky tests”:
- tests pass sometimes
- tests fail sometimes
- and debugging becomes painful

## Part E — The Correct Pattern: Fresh Object Per Test

### Approach 1: Explicitely create a new object in each test

```python
class TestPotionShopFresh(unittest.TestCase):

    def test_buy_health(self):
        shop = PotionShop(100)
        shop.buy("health")
        self.assertEqual(shop.count("health"), 4)
        self.assertEqual(shop.gold, 90)

    def test_buy_mana(self):
        shop = PotionShop(100)
        shop.buy("mana")
        self.assertEqual(shop.count("mana"), 3)
        self.assertEqual(shop.gold, 85)
```

### Approach 2: The Professional Way

#### Why use `setup()`?
When you need the same starting state for many tests, you can use `setup()` to move repitition .

```python
class TestPotionShopSetup(unittest.TestCase):

    def setUp(self):
        print("Setup your instance")
        self.shop = PotionShop(100)

    def test_buy_health(self):
        self.shop.buy("health")
        self.assertEqual(self.shop.count("health"), 4)
        self.assertEqual(self.shop.gold, 90)

    def test_buy_mana(self):
        self.shop.buy("mana")
        self.assertEqual(self.shop.count("mana"), 3)
        self.assertEqual(self.shop.gold, 85)

    def test_count_unknown_kind(self):
        self.assertEqual(self.shop.count("stamina"), 0)
```
> <mark>`setUp()` runs before every test method.</mark>

__Questions:__ 
1. How many times does `setUp()` run if you have 3 tests?
2. Is `self.shop` the same object across tests? Why or why not?
3. Why is this better than repeating `shop = PotionShop(100)` in each test?

#### Why use `teardown()`?
Use it when you need to clean up external resources such as:
- files you created
- database connections
- network resources
- temporary directories

For `PotionShop`, you don’t need it—but we’ll include it to teach the pattern.
```python
class TestPotionShopTeardown(unittest.TestCase):
     count = 0
     def setUp(self):
        print(f"Setup instance no. {self.count}")
        self.shop = PotionShop(100)
        count += 1

    def tearDown(self):
        print("Setup your instance")
```

#### Exercise 1
Use `setup()` to test the following sequence of operations:
- Start with 100 `gold`
- Buy `health`
- Buy `mana`
- Buy `mana`

Expected final state:
- `gold` should be 100 - 10 - 15 - 15 = 60
- `health` count should be 4
- `mana` count should be 4

#### Exercise 2
Consider the upgraded version of buy such that,
- buying an unknown potion raises `keyError`
- buying when gold is insufficient raises `ValueError`

```python
def buy(self, kind):
    if kind not in self.prices:
        raise KeyError("Unknown potion type.")
    if self.gold < self.prices[kind]:
        raise ValueError("Not enough gold.")
    self.gold -= self.prices[kind]
    self.inventory[kind] += 1
    return f"bought {kind}"
```

Write two tests:
- buying `"speed"` raises ValueError
- starting with 5 gold and buying `"health"` raises `ValueError`
