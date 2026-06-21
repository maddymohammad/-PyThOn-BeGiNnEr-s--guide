# 07 · Loops — Solutions

Answers for the 30 questions in [`topics/07-loops.md`](../topics/07-loops.md).

---

**1. Iterable.**
Something you can loop over, yielding one item at a time. Examples: a list, a string, a `range`, a
tuple, a dictionary, a set.

**2. `for` loop difference.**
Python's `for` iterates the items directly (`for x in items`), so you don't create or manage an index
counter; in many languages you loop on an integer index and look the item up.

**3. `range(5)`.**
`0, 1, 2, 3, 4`.

**4. `range(2, 6)`.**
`2, 3, 4, 5`.

**5. `range(0, 10, 2)`.**
`0, 2, 4, 6, 8`.

**6. Count down 5 → 1.**
```python
for i in range(5, 0, -1):
    print(i)
```

**7. Five iterations stopping at 4.**
`range(5)` generates `0, 1, 2, 3, 4` — the stop value `5` is exclusive, so it's never produced.

**8. When to use `while`.**
When you don't know in advance how many iterations you need and you loop until some condition changes
(e.g. "keep asking until the input is valid").

**9. Infinite loop cause.**
Forgetting to update the variable the condition depends on, so the condition never becomes false.

**10. `break` and `continue`.**
`break` exits the loop entirely; `continue` skips the rest of the current iteration and moves to the
next one.

**11. Predicted output.**
```
0
1
2
```
It prints 0, 1, 2, then `break`s when `n == 3`.

**12. Predicted output.**
```
1
3
```
Even numbers hit `continue` and are skipped.

**13. Loop `else`.**
It runs only if the loop completed normally — i.e. it was **not** terminated by `break`.

**14. Predicted output.**
```
not found
```
No element equals 10, so `break` never fires and the `else` runs.

**15. Search with `for`/`else`.**
```python
for n in numbers:
    if n == 7:
        print("found")
        break
else:
    print("missing")
```

**16. `enumerate(["a", "b"])`.**
Pairs of `(index, value)`: `(0, "a")` then `(1, "b")`.

**17. Start at 1.**
```python
enumerate(items, start=1)
```

**18. Why `range(len(...))` is un-Pythonic.**
It reintroduces manual index bookkeeping that `for x in items` (or `enumerate`) removes. It's more
verbose and more error-prone, and it doesn't read as clearly.

**19. `zip([1, 2, 3], ["a", "b"])`.**
`(1, "a")` and `(2, "b")` — two pairs. `zip` stops at the shortest iterable, so the trailing `3` is
dropped.

**20. Parallel loop.**
```python
for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

**21. Iterating a dict directly.**
You get the **keys**.

**22. Keys and values together.**
```python
for key, value in d.items():
    ...
```

**23. 3×3 grid of `*`.**
```python
for _ in range(3):
    for _ in range(3):
        print("*", end="")
    print()
```

**24. Inner block count.**
`3 × 3 = 9` times.

**25. Mutating while looping.**
Removing items shifts the remaining elements' positions while the loop is still advancing by index,
so some elements get skipped and the result is wrong.

**26. Keep only odds (safe).**
```python
nums = [n for n in nums if n % 2 != 0]
```

**27. `while` 1 → 5.**
```python
i = 1
while i <= 5:
    print(i)
    i += 1
```

**28. Sum 1 → 100.**
```python
total = 0
for n in range(1, 101):
    total += n
print(total)   # 5050
```

**29. Characters with index.**
```python
for i, ch in enumerate("hello"):
    print(i, ch)
```

**30. FizzBuzz 1–15.**
```python
for n in range(1, 16):
    if n % 15 == 0:
        print("FizzBuzz")
    elif n % 3 == 0:
        print("Fizz")
    elif n % 5 == 0:
        print("Buzz")
    else:
        print(n)
```
(Check the combined `% 15` case first, or it would never be reached.)
