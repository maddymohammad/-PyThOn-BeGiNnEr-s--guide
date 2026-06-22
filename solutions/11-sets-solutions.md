# 11 · Sets — Solutions

Answers for the 30 questions in [`topics/11-sets.md`](../topics/11-sets.md).

---

**1. Three properties.**
A set is **unordered**, holds **unique** elements, and those elements must be **hashable**. (It's also
mutable.)

**2. Two advantages.**
It automatically removes duplicates, and membership testing (`x in s`) is fast — average O(1),
roughly constant regardless of size.

**3. Empty set.**
`set()`. You can't use `{}` because that creates an empty **dictionary**.

**4. Types.**
`{}` → `dict`; `set()` → `set`.

**5. `set([1, 1, 2, 3])`.**
`{1, 2, 3}` — duplicates are dropped.

**6. De-duplicate.**
```python
list(set([1, 1, 2, 3, 3]))   # {1,2,3} -> e.g. [1, 2, 3] (order not guaranteed)
```

**7. `s[0]` fails.**
Sets are unordered and not subscriptable, so there's no "position 0" to index. It raises `TypeError`.

**8. Print order.**
No — set order isn't guaranteed. Small integer sets often *look* sorted, but that's an implementation
detail you must not depend on.

**9. `.remove()` vs `.discard()`.**
Both delete an element, but `.remove(x)` raises `KeyError` if `x` isn't present, while `.discard(x)`
does nothing (no error) in that case.

**10. `.pop()` on a set.**
It removes and returns an element, but the element is **arbitrary** — not necessarily the first or
smallest — because sets have no order.

**11. Add 4.**
```python
{1, 2, 3}.add(4)   # {1, 2, 3, 4}
```

**12. Union.**
`{1, 2, 3, 4}`.

**13. Intersection.**
`{2, 3}`.

**14. Difference.**
`{1}`.

**15. Symmetric difference.**
`{1, 4}`.

**16. Symmetric difference meaning.**
The elements that are in exactly one of the two sets — in one or the other, but not in both.

**17. Union operator/method.**
The `|` operator and the `.union()` method.

**18. Subset.**
```python
{1, 2} <= {1, 2, 3}   # True
```

**19. Superset.**
```python
{1, 2, 3} >= {1, 2}   # True
```

**20. Disjoint.**
```python
{1, 2}.isdisjoint({3, 4})   # True
```

**21. Membership test.**
```python
2 in {1, 2, 3}   # True
```
It's fast because sets use a hash table, giving average O(1) lookups.

**22. Speed comparison.**
Set membership stays roughly constant as the collection grows (O(1) average), while list membership
gets slower in proportion to length (O(n)).

**23. `len()`.**
The number of (unique) elements.

**24. `{1, [2, 3]}`.**
Raises `TypeError: unhashable type: 'list'` — a list is mutable and unhashable, so it can't be a set
element.

**25. `frozenset`.**
An immutable set. Because it's hashable, it can be stored inside another set or used as a dictionary
key — things a normal (mutable) set cannot do.

**26. Set comprehension.**
```python
{x * 2 for x in range(5)}   # {0, 2, 4, 6, 8}
```

**27. `{1, 2, 2, 3}`.**
No duplicate survives — the set is `{1, 2, 3}`, and its length is `3`.

**28. Values in both.**
```python
set(a) & set(b)
```

**29. In `a` but not `b`.**
```python
set(a) - set(b)
```

**30. Many membership tests.**
Convert the list to a set first (`lookup = set(big_list)`), then test `x in lookup`. Set lookups are
O(1) on average, so thousands of checks become far cheaper than repeatedly scanning the list.
