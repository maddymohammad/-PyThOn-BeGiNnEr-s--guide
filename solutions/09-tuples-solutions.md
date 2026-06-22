# 09 · Tuples — Solutions

Answers for the 30 questions in [`topics/09-tuples.md`](../topics/09-tuples.md).

---

**1. Two properties.**
A tuple is **ordered** and **immutable**.

**2. Parentheses or comma.**
The comma. `(5)` is just the integer `5` (the parentheses only group), while `(5,)` is a one-element
tuple. `type((5))` is `int`; `type((5,))` is `tuple`.

**3. Types.**
`(5)` → `int`; `(5,)` → `tuple`.

**4. Three ways.**
```python
a = (1, 2, 3)        # with parentheses
b = 1, 2, 3          # without parentheses (packing)
c = tuple("ab")      # from a string -> ('a', 'b')
```

**5. Empty tuple.**
```python
()          # or  tuple()
```

**6. Index and slice.**
`t[0]` → `10`; `t[-1]` → `40`; `t[1:3]` → `(20, 30)`.

**7. `t[0] = 99`.**
Raises `TypeError` — tuples are immutable, so you can't assign to an element.

**8. Predicted output.**
```
([1, 2, 9], 3)
```

**9. Why it's allowed.**
The tuple's slot still points to the *same* list object; you're mutating that list's contents, not
replacing the tuple's reference. Immutability applies to the tuple's own structure, not to mutable
objects stored inside it.

**10. Unpack.**
```python
x, y = (3, 4)
```

**11. Swap connection.**
`a, b = b, a` packs `b, a` into a tuple `(b, a)` and then unpacks it into `a, b`, which swaps them
without a temporary variable.

**12. `first, *rest = (1, 2, 3, 4)`.**
`first = 1`, `rest = [2, 3, 4]`.

**13. List or tuple.**
`rest` is a **list**, even though the right-hand side was a tuple.

**14. `first, *middle, last`.**
`first = 1`, `middle = [2, 3, 4]`, `last = 5`.

**15. Returning multiple values.**
By returning them separated by commas, which packs them into a tuple: `return a, b`.

**16. `divmod(17, 5)`.**
Returns `(3, 2)` — a `tuple` of (quotient, remainder).

**17. min/max function.**
```python
def min_max(nums):
    return min(nums), max(nums)

low, high = min_max([3, 1, 7])   # low=1, high=7
```

**18. Only two methods.**
Because tuples are immutable, methods that would modify them (append, sort, remove, …) don't exist.
The two non-modifying ones are `.count()` and `.index()`.

**19. `.count(2)`.**
`2`.

**20. `.index(2)`.**
`1`.

**21. `+` and `*`.**
`(1, 2) + (3,)` → `(1, 2, 3)`; `(0,) * 3` → `(0, 0, 0)`.

**22. Tuple/list as dict key.**
A tuple can be a dict key because it's hashable (immutable); a list cannot because it's mutable and
therefore unhashable.

**23. Condition for a tuple key.**
Every element inside the tuple must itself be hashable (so a tuple containing a list still can't be a
key).

**24. Tuple over list.**
Any two of: the data is a fixed record (e.g. coordinates), you need a dict key or set element, you
want to guarantee it won't be modified.

**25. List over tuple.**
Any two of: the collection changes over time, you need methods like `append`/`sort`, or you're
collecting a growing sequence of similar items.

**26. `len()` and `in`.**
Yes to both — neither modifies the tuple.

**27. Sorting a tuple.**
There's no `.sort()` method (it would mutate). Use the `sorted()` function, which returns a new
**list**: `sorted((3, 1, 2))` → `[1, 2, 3]` (convert back with `tuple(...)` if needed).

**28. `x = (5); print(x + 1)`.**
Prints `6`. `(5)` is the integer `5`, not a tuple, so `x + 1` is `5 + 1`.

**29. List as a key.**
Raises `TypeError: unhashable type: 'list'`.

**30. Round-trip via list.**
```python
t = (1, 2, 3)
lst = list(t)      # [1, 2, 3]
lst.append(4)      # [1, 2, 3, 4]
t = tuple(lst)     # (1, 2, 3, 4)
```
