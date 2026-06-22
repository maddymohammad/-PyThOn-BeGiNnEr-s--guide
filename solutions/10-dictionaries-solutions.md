# 10 · Dictionaries — Solutions

Answers for the 30 questions in [`topics/10-dictionaries.md`](../topics/10-dictionaries.md).

---

**1. What it stores.**
Key → value pairs. The two halves are the **key** and the **value**.

**2. Ordered?**
Yes — dictionaries preserve insertion order as of Python 3.7.

**3. Key rules.**
Keys must be **unique** and **hashable** (immutable types like str, int, tuple).

**4. Repeats.**
A value can repeat across keys; a key cannot — assigning a duplicate key overwrites the earlier value.

**5. List vs tuple key.**
A list is mutable and therefore unhashable, so it can't be a key. A tuple is immutable (hashable), so
it can — provided its elements are hashable too.

**6. Two ways.**
```python
a = {"x": 1, "y": 2}
b = dict(x=1, y=2)        # or dict([("x", 1), ("y", 2)])
```

**7. Missing key with `[]`.**
Raises `KeyError`.

**8. Safe lookup.**
```python
person.get("email")       # None if absent
```

**9. With a default.**
```python
person.get("email", "unknown")
```

**10. Add a key.**
```python
person["city"] = "London"
```

**11. Assigning an existing key.**
It overwrites that key's value (keys are unique).

**12. Predicted output.**
```
{'a': 2}
```

**13. Three removals.**
`del d[key]`, `d.pop(key)`, and `d.clear()` (also `.popitem()`). `del` removes the pair and returns
nothing; `.pop(key)` removes it and **returns the value**.

**14. `.pop("age")`.**
Returns the value `36` and removes that pair, leaving `{'name': 'Ada'}`.

**15. `.popitem()`.**
Removes and returns the **last inserted** `(key, value)` pair as a tuple.

**16. View methods.**
`.keys()` → keys, `.values()` → values, `.items()` → `(key, value)` pairs. They're called *views*
because they stay in sync with the dict — change the dict and the view reflects it.

**17. Keys to list.**
```python
list(d.keys())
```

**18. `for k in d:`.**
You iterate the **keys**.

**19. Print every pair.**
```python
for key, value in d.items():
    print(f"{key}: {value}")
```

**20. Modifying during iteration.**
Adding or removing keys mid-iteration raises a `RuntimeError` because the dict's size changes under
the loop. Iterate over a snapshot instead: `for k in list(d.keys()):`.

**21. `"apple" in prices`.**
Checks **keys**.

**22. Check a value.**
```python
50 in prices.values()
```

**23. `len()`.**
The number of key–value pairs.

**24. Merge two ways.**
```python
{**{"x": 1, "y": 2}, **{"y": 9, "z": 3}}   # {'x': 1, 'y': 9, 'z': 3}
{"x": 1, "y": 2} | {"y": 9, "z": 3}        # same (Python 3.9+)
```

**25. Conflict winner.**
The right-hand dictionary's value wins.

**26. `setdefault`.**
If `"A"` is missing, it inserts `"A": []` and returns that new list. If `"A"` already exists, it leaves
it untouched and returns the existing value.

**27. Squares comprehension.**
```python
{n: n * n for n in range(5)}   # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

**28. Filter comprehension.**
```python
{k: v for k, v in prices.items() if v < 30}
```

**29. `{"a": 1, "a": 2}`.**
Evaluates to `{'a': 2}`. The duplicate key isn't an error; the later value simply replaces the earlier
one.

**30. Vote counter.**
```python
votes = ["yes", "no", "yes", "yes"]
counts = {}
for v in votes:
    counts[v] = counts.get(v, 0) + 1
# {'yes': 3, 'no': 1}
```
