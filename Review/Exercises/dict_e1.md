**Exercise 1:** What would be the return values of the given methods cosidering the dictionary:
```
my_info = {'name': 'SOMEONE', 'city': 'SOMEWHERE', 'state': 'ANYWHERE'}
```
- `my_info.keys()`
- `my_info.values()`
- `my_info.items()`
- `my_info.get('name', 'NA')`
- `my_info.get('occupation', 'TRAVELER')`

</br>

**Exercise 2:** Given the following two dictionaries:
```
md1 = {'Ten': 10, 'Twenty': 20, 'Thirty': 30}
md2 = {'Thirty': 300, 'Fourty': 40, 'Fifty': 50}
```
Merge these dictionaries into a new dictionary named `comb_md` using the `items()` method.

Then answer the following questions:
- How many key–value pairs does `comb_md` contain?
- What is the value associated with the key `'Thirty'` in `comb_md`?

</br>

**Exercise 3:** Create a frequency dictionary of the given list:
- without using the `get()` method,
- using the `get()` method.
```
my_list = [1, 2, 2, 4, 8, 4, 4, 8, 8]
```

</br>

**Exercise 4:** First Repeating Element

Given an array `arr`, your task is to find the index of the first repeating element. 
A repeating element is one that appears more than once, and you must return the index of its first occurrence. If no element repeats, return `0`.

Example:
- Input: `arr = [1, 5, 3, 4, 3, 5, 6]`
- Output: `1`
- Reason: 5 is the first repeating number, which can be first seen at index 1.

</br>

**Exercise 5:** Group Anagrams

Given a list of strings `strs`, group the anagrams together. You can return the answer in any order.

Example:
- Input: `strs = ["eat","tea","tan","aTe","Nat","bat"]`
- Output: `[["bat"],["Nat","tan"],["aTe","eat","tea"]]`

***Note:*** A string is an anagram of another string if it can be formed by rearranging the characters in the first string 
(using all of the characters exactly the number of times they occur in the first string).

Example:
- `'act'` and `'cat'` are anagrams.
- `'state'` and `'taste'` are anagrams.
- `'states'` and `'taste'` are not anagrams as `'states'` has two `'s'` characters but `'taste'` only has one `'s'`.

**Hint:**

- A common strategy for detecting anagrams is to sort the characters of each string and use the sorted result as a key.

Example:
```
sorted("eat")   → ['a', 'e', 't']
sorted("tea")   → ['a', 'e', 't']
```
Since the sorted character lists match, the words are anagrams.

- Be careful with uppercase and lowercase letters. In Python, uppercase and lowercase characters are treated as different:
```
sorted("Nat")   → ['N', 'a', 't']
sorted("tan")   → ['a', 'n', 't']
```
To correctly group anagrams regardless of case, you may need to convert strings to the same case before sorting, for example:
```
sorted("Nat".lower()) → ['a', 'n', 't']
```
