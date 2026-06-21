# 08 · Lists — Solutions

Answers for the 30 questions in [`topics/08-lists.md`](../topics/08-lists.md).

---

**1. Two properties.**
A list is **ordered** (items keep their position) and **mutable** (you can change it in place).

**2. Mixed types.**
Yes. e.g. `[1, "two", 3.0, True]`.

**3. String to list.**
```python
list("abc")   # ['a', 'b', 'c']
```

**4. Index and slice.**
`items[-1]` → `'d'`; `items[1:3]` → `['b', 'c']`.

**5. Slicing and the original.**
Slicing does **not** modify the original; it returns a new list (a shallow copy of that section).

**6. Change the second item.**
```python
items[1] = "X"
```

**7. `append` vs `extend`.**
`.append` adds its argument as a single element; `.extend` adds each element of an iterable.
```python
a = [1, 2]; a.append([3, 4])   # [1, 2, [3, 4]]
b = [1, 2]; b.extend([3, 4])   # [1, 2, 3, 4]
```

**8. `.pop()` vs `.remove()`.**
`.pop()` removes and **returns** an item (last by default, or at a given index). `.remove(x)` deletes
the first item equal to `x` and returns `None`.

**9. `[1, 2].remove(9)`.**
A `ValueError` (the value isn't in the list).

**10. `result = [3, 1, 2].sort()`.**
`result` is `None`. `.sort()` sorts in place and returns `None`, so assigning its return value
discards the data. This is the most common list bug.

**11. New sorted list.**
```python
sorted([3, 1, 2])   # [1, 2, 3]
```

**12. Sort by length.**
```python
words.sort(key=len)   # ['fig', 'pear', 'banana']
```

**13. Descending.**
```python
sorted([1, 2, 3], reverse=True)   # [3, 2, 1]
```

**14. `+` and `*`.**
`[1, 2] + [3, 4]` → `[1, 2, 3, 4]`; `[0] * 3` → `[0, 0, 0]`.

**15. Membership.**
```python
5 in some_list
```

**16. Aggregates on `[3, 1, 2]`.**
`len` → `3`, `sum` → `6`, `min` → `1`, `max` → `3`.

**17. Squares comprehension.**
```python
[n * n for n in range(5)]   # [0, 1, 4, 9, 16]
```

**18. Evens comprehension.**
```python
[n for n in range(10) if n % 2 == 0]   # [0, 2, 4, 6, 8]
```

**19. Why comprehensions are preferred.**
They're shorter, read as a single intent ("a list of X for each Y"), and are typically faster than
repeatedly calling `.append()` in a loop.

**20. Access `6`.**
```python
grid[1][2]
```

**21. Aliasing prediction.**
```
[1, 2, 3, 4]
```
`b = a` makes `b` another name for the same list, so appending through `b` also changes `a`.

**22. Independent copy (two ways).**
```python
b = a.copy()
b = a[:]          # or  b = list(a)
```

**23. Multiplication trap prediction.**
```
[[1, 0, 0], [1, 0, 0], [1, 0, 0]]
```
`[[0] * 3] * 3` makes three references to the *same* inner list, so setting `grid[0][0] = 1` changes
every row.

**24. Correct 3×3 grid.**
```python
grid = [[0] * 3 for _ in range(3)]
```

**25. Shallow vs deep copy.**
A shallow copy duplicates the outer list but still shares any nested objects (inner lists). A deep
copy (`copy.deepcopy`) recursively duplicates everything, so nested data is independent too.

**26. Insert at index 1.**
```python
["a", "b", "c"].insert(1, "x")   # ['a', 'x', 'b', 'c']
```

**27. Empty the list.**
```python
some_list.clear()
```

**28. `.count(2)`.**
`2`.

**29. Reverse in place.**
```python
nums = [1, 2, 3]
nums.reverse()   # nums is now [3, 2, 1]; the method returned None
```

**30. Double odds, drop evens.**
```python
[n * 2 for n in nums if n % 2 != 0]   # for [1,2,3,4,5] -> [2, 6, 10]
```
