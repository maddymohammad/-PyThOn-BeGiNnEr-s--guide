# 12 · Functions — Solutions

Answers for the 30 questions in [`topics/12-functions.md`](../topics/12-functions.md).

---

**1. Defining keyword.**
`def`. The indented lines beneath the `def` header form the body.

**2. Parameter vs argument.**
A **parameter** is the variable named in the definition; an **argument** is the actual value passed
when the function is called.

**3. `add`.**
```python
def add(a, b):
    return a + b

add(2, 3)   # 5
```

**4. No `return`.**
The function returns `None`.

**5. `x = print("hi")`.**
It prints `hi`, and `x` is `None` — because `print()` returns `None`.

**6. Print vs return.**
Printing displays text on the screen for a human to read; returning hands a value back to the calling
code so it can be stored or used further. Printing produces no usable value.

**7. What else `return` does.**
It immediately exits the function — any code after the executed `return` is skipped.

**8. First even.**
```python
def first_even(numbers):
    for n in numbers:
        if n % 2 == 0:
            return n
    return None
```

**9. Multiple values.**
Separate them with commas in the `return` (they're packed into a tuple), then unpack on the receiving
side: `low, high = min_max(nums)`.

**10. Default greeting.**
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"
```

**11. `def f(a=1, b)`.**
It's a `SyntaxError`. Rule: parameters with defaults must come **after** all parameters without
defaults.

**12. All keywords, reordered.**
```python
describe(city="London", name="Ada", age=36)
```

**13. Positional after keyword.**
No — it's a `SyntaxError`. Once a keyword argument appears in a call, all following arguments must be
keywords too.

**14. `*args`.**
It collects any extra positional arguments into a **tuple**.

**15. `**kwargs`.**
It collects any extra keyword arguments into a **dict**.

**16. `total`.**
```python
def total(*args):
    return sum(args)
```

**17. Unpack into the call.**
```python
total(*nums)   # same as total(1, 2, 3)
```

**18. Parameter order.**
Positional parameters, then `*args`, then keyword-only parameters, then `**kwargs`.

**19. Predicted output.**
A `NameError` — `x` is local to `f`, so it doesn't exist at the `print(x)` line outside the function.

**20. Reading vs reassigning a global.**
A function can **read** a global without any keyword. Reassigning one requires the `global` keyword;
otherwise the assignment creates a new local variable instead.

**21. `global`.**
The `global` keyword. Use it sparingly because functions that mutate globals are harder to test and
reason about; passing values in and returning results is usually cleaner.

**22. LEGB.**
Local, Enclosing, Global, Built-in — the order Python searches scopes to resolve a name.

**23. `UnboundLocalError`.**
Assigning to `count` anywhere in the function makes `count` local for the whole function. So
`count += 1` tries to read the local `count` before it's been assigned, which raises
`UnboundLocalError`. Declaring `global count` fixes it.

**24. Mutable-default output.**
```
[1]
[1, 2]
```
The default list is created once and reused, so the second call sees the item left by the first.

**25. Why the bug happens.**
Default argument values are evaluated **once**, when the function is defined — not on each call. A
mutable default (a list) therefore persists and accumulates across calls.

**26. Correct `add_item`.**
```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

**27. Docstring.**
A string literal placed as the first line of the function body. It documents the function and is what
`help()` (and many tools/IDEs) display.

**28. Square lambda.**
```python
square = lambda x: x * x
square(5)   # 25
```

**29. Lambda vs def.**
Use a `lambda` for a tiny, single-expression function needed briefly (like a `key=` argument). Use a
normal `def` for anything longer or reused — it's clearer and can carry a docstring.

**30. Type hints at runtime.**
Nothing — they're not enforced at runtime. They serve as documentation for readers and let tools
(linters, type checkers, IDEs) catch mismatches.
