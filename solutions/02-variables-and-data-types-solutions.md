# 02 · Variables & Data Types — Solutions

Answers for the 30 questions in
[`topics/02-variables-and-data-types.md`](../topics/02-variables-and-data-types.md).

---

**1. Dynamically typed.**
The type belongs to the value, not the name; a name can be rebound to a different type at any time.
```python
x = 10      # x refers to an int
x = "ten"   # now the same name refers to a str — perfectly legal
```

**2. `2name = 5`?**
Invalid (`SyntaxError`). Identifiers cannot start with a digit.

**3. `total` vs `Total`.**
Different variables. Python is case-sensitive.

**4. PEP 8 variable style.**
`snake_case` (lowercase words joined by underscores).

**5. Signalling a constant.**
Name it in `UPPER_SNAKE_CASE`, e.g. `MAX_RETRIES = 5`.

**6. Are constants enforced?**
No. The uppercase name is only a convention — a promise not to reassign. Python will happily let you
change it.

**7. Numeric types.**
`int` (`42`), `float` (`3.14`), `complex` (`2 + 3j`).

**8. `type(3.0)`.**
`<class 'float'>` — the decimal point makes it a float, not an int.

**9. `type()` vs `isinstance()`.**
`type()` returns the exact type object; `isinstance(obj, T)` returns `True`/`False` and also accepts
subclasses and a tuple of types. Prefer `isinstance()` in real code because it handles inheritance
and is more flexible.

**10. `isinstance(True, int)`.**
`True`. `bool` is a subclass of `int`, so a boolean *is* an integer as far as the type system is
concerned.

**11. `True + True + True`.**
`3`. Booleans behave as `1`/`0` in arithmetic, so it's `1 + 1 + 1`.

**12. No overflow.**
Python's `int` has arbitrary precision — it grows to fit. `2 ** 100` returns the full number
`1267650600228229401496703205376`, not an error.

**13. Readable million.**
```python
1_000_000
```
Underscores are ignored by Python and are purely for human readability.

**14. `None`.**
Its type is `NoneType`, and there is exactly one `None` object (a singleton).

**15. `is None` vs `== None`.**
Because `None` is a unique singleton, identity (`is`) is the correct, fastest, and idiomatic check.
`==` could in theory be overridden by a custom class to give misleading results.

**16. Four falsy values.**
Any four of: `False`, `None`, `0`, `0.0`, `""`, `[]`, `()`, `{}`, `set()`.

**17. `if "0":`.**
Prints `yes`. The string `"0"` is non-empty, so it is truthy — its *contents* don't matter, only
whether it's empty.

**18. `bool([])`.**
`False`. An empty list is falsy. Empty containers are always falsy.

**19. `"42"` + 8.**
```python
int("42") + 8   # 50
```

**20. `int("3.9")`.**
Raises `ValueError` — `int()` can parse an integer string but not a float-looking string. To get `3`:
```python
int(float("3.9"))   # 3
```

**21. `int(3.9)`.**
Truncates toward zero; it does **not** round. Result: `3`. (Use `round(3.9)` → `4` if you want
rounding.)

**22. `100` to string.**
```python
str(100)   # "100"
```
You'd need it to join a number into a message, e.g. `"You have " + str(100) + " points"`, since you
can't concatenate a string and an int directly.

**23. `list("cat")`.**
`['c', 'a', 't']` — strings are iterable, so `list()` splits into individual characters.

**24. `==` vs `is`.**
`==` compares *value* (are the contents equal?). `is` compares *identity* (are they the same object
in memory?).

**25. `a == b, a is b`.**
Prints `True False`. The two lists have equal contents (`==` is `True`) but are distinct objects in
memory (`is` is `False`).

**26. Small-integer caching.**
CPython pre-creates and reuses integer objects roughly in the range `-5` to `256`, so two variables
holding the same small int may share one object and compare `True` with `is`. Outside that range they
usually don't. It's an implementation detail and varies, so never use `is` to compare integer values —
use `==`.

**27. Immutable types.**
Any four of: `int`, `float`, `complex`, `bool`, `str`, `tuple`, `frozenset`, `bytes`, `NoneType`.

**28. Mutable types.**
Any three of: `list`, `dict`, `set`, `bytearray`.

**29. Swap in one line.**
```python
a, b = b, a
```

**30. `x = y = []` then `x.append(1)`.**
`y` is `[1]`. Both names refer to the **same** list object, so mutating it through `x` is visible
through `y`. This is the single most common mutability surprise in Python.
