## **Mutable vs. Immutable Data Types**

In Python, everything is an object, but not all objects behave the same. The key difference: ***mutability***.

---

### **Immutable Objects** 

Cannot be changed once created. Examples: `int`, `float`, `str`, `tuple`.

The following code creates a new string object `"cats"`, the old `"cat"` is unchanged.
```
word = "cat"
word = word + "s"
print(word)
```

</br>

***How does this code work?***

- Step 1: Create the first object (`cat`) and bind the name (word)

  *  Code: `word = "cat"`
  *  Python makes a string object that holds the characters `c a t`.
  *  The name `word` is now bound (points) to that object.
  *  Think of `word` as a sticky note with the label "word" stuck onto the `cat` object.

  ```
  word ──▶  "cat"
  ```

- Step 2: Build a new string during concatenation

  * Code: `word + "s"`
  * Python looks up what word refers to (the `cat` object).
  * `s` is another string object.
  * Because strings are immutable (cannot be changed), Python does NOT add the letter onto the existing `cat` object.
  * Instead, it creates a brand-new string: `cats`.

  ```
  word ──▶  "cat"      "s"
                 ╲     /
                  ╲   /
                 (makes new) ──▶ "cats"
  ```

- Step 3: Rebind the name (`word`) to the new object (`cats`)

  * Code: `word = word + "s"`
  * The new `cats` object is created (from step 2).
  * Now Python rebinds the name `word` so it points to `cats`.
  * The old `cat` object is left behind. Since no other names point to it, Python will clean it up later (garbage collection).

  ```
  word ──▶  "cats"
  ("cat" is now unreferenced and may be cleaned up later)
  ```
  *Important*: The original "cat" object was not changed. We simply moved the sticky note word from "cat" to "cats".

---

### **Mutable Objects**

Can be changed after creation. Examples: `list`, `dict`, `set`.

In the following code, we didn't create a new list object, rather, the same list object was modified.
```
pets = ["cat", "dog", "hamster"]
pets[0] = "parrot"
print(pets)
```


***How does this code work?***

- Step 1: Create the first list object and bind the name (`pets`)

  * Code: `pets = ["cat", "dog", "hamster"]`
  * Python makes a list object in memory containing three elements.
  * The name `pets` is bound to this list object.

  ```
  pets ──▶ ["cat", "dog", "hamster"]
  ```

- Step 2: Modify the list in place

  * Code: `pets[0] = "parrot"`
  * Python looks at the object that `pets` points to.
  * Lists are mutable, so instead of making a new list, Python updates the existing list directly.
  * The first element `cat` is replaced by `parrot`.
  * Important: the list object in memory does not move or change identity. Its contents change.

  ```
  pets ──▶ ["parrot", "dog", "hamster"]
  (Same list object, just updated inside.)
  ```
