# 02 · Variables & Data Types

> **You will be able to:** create variables, name them well, identify Python's core data types,
> convert between them, and explain the difference between mutable and immutable objects.

---

## What is a variable?

A variable is a **name that refers to a value**. In Python you create one simply by assigning to it
with `=`:

```python
age = 25
name = "Ada"
price = 19.99
is_member = True
```

There is no separate "declaration" step and you never state the type — Python infers it. A useful
mental model: the variable is a *label* stuck onto an object in memory, not a box that contains the
value. This matters later when we discuss mutability.

```python
x = 10        # x labels the integer 10
x = "ten"     # the same name can later label a completely different type
```

This is what **dynamic typing** means: the *name* has no fixed type, the *value* does.

---

## Naming rules and conventions

| Rule (required)                                  | Example                          |
|--------------------------------------------------|----------------------------------|
| May contain letters, digits, underscores         | `user_name`, `count2`            |
| Must **not** start with a digit                  | `2nd` ✗ → `second` ✓             |
| Case-sensitive                                   | `age` and `Age` are different    |
| Cannot be a reserved keyword                     | `class`, `for`, `if`, `True` ✗   |

| Convention (PEP 8, not enforced)                 | Example                          |
|--------------------------------------------------|----------------------------------|
| Variables & functions use `snake_case`           | `total_price`, `get_user()`      |
| Constants use `UPPER_SNAKE_CASE`                  | `MAX_SIZE = 100`                 |
| Names should be descriptive                       | `n` ✗ for a user count → `user_count` ✓ |

> **Watch out:** Python has no true constants — `UPPER_SNAKE_CASE` is a *promise* to other
> programmers that you won't reassign the value, not something the language enforces.

You can see the reserved keywords yourself:

```python
import keyword
print(keyword.kwlist)
```

---

## The core built-in types

| Type        | Category    | Example            | Mutable? |
|-------------|-------------|--------------------|----------|
| `int`       | Number      | `42`, `-7`         | No       |
| `float`     | Number      | `3.14`, `2.0`      | No       |
| `complex`   | Number      | `2 + 3j`           | No       |
| `bool`      | Boolean     | `True`, `False`    | No       |
| `str`       | Text        | `"hello"`          | No       |
| `list`      | Sequence    | `[1, 2, 3]`        | **Yes**  |
| `tuple`     | Sequence    | `(1, 2, 3)`        | No       |
| `dict`      | Mapping     | `{"a": 1}`         | **Yes**  |
| `set`       | Collection  | `{1, 2, 3}`        | **Yes**  |
| `frozenset` | Collection  | `frozenset({1,2})` | No       |
| `NoneType`  | Special     | `None`             | No       |

You will meet lists, tuples, dicts, and sets in their own lessons. For now, focus on numbers,
strings, booleans, and `None`.

### Checking a type

```python
print(type(42))        # <class 'int'>
print(type("hi"))      # <class 'str'>
print(type(3.0))       # <class 'float'>
```

Use `type()` to *see* the exact type, but use `isinstance()` to *test* a type in real code:

```python
isinstance(42, int)        # True
isinstance(True, int)      # True  (see the gotcha below)
isinstance(3.0, (int, float))  # True — accepts a tuple of types
```

> **Watch out — a classic interview trap:** `bool` is a *subclass* of `int`. So `True == 1` is
> `True`, `False == 0` is `True`, and `True + True` is `2`. `isinstance(True, int)` returns `True`.

---

## Numbers in brief

```python
a = 7          # int
b = 7.0        # float (note the decimal point)
c = 2 + 3j     # complex
```

- `int` has **unlimited precision** in Python — `2 ** 1000` just works, no overflow.
- `float` is a 64-bit decimal approximation, so it has rounding quirks (lesson 03 covers
  `0.1 + 0.2`).
- You can write large numbers readably with underscores: `1_000_000`.

---

## `None`

`None` is a special object meaning "no value" or "nothing here yet." It is its own type
(`NoneType`) and there is only ever one of it.

```python
result = None
print(result is None)   # True — the idiomatic way to check for None
```

> **Watch out:** Always test with `is None`, never `== None`. `is` checks identity, which is exactly
> right for the single `None` object.

---

## Truthy and falsy

Every value in Python is either "truthy" or "falsy" when used in a boolean context (like an `if`).

| Falsy (treated as `False`)                  | Everything else is truthy            |
|---------------------------------------------|--------------------------------------|
| `False`, `None`                             | non-zero numbers (`1`, `-5`, `3.14`) |
| `0`, `0.0`, `0j`                            | non-empty strings (`"hi"`)           |
| `""` (empty string)                         | non-empty containers (`[0]`, `{0}`)  |
| `[]`, `()`, `{}`, `set()` (empty containers)| the object `True`                    |

```python
name = ""
if name:
    print("has a name")
else:
    print("empty")   # this runs, because "" is falsy
```

You can check explicitly with `bool(value)`:

```python
bool(0)      # False
bool("")     # False
bool("no")   # True  (any non-empty string is truthy, even the word "no")
```

---

## Type conversion (casting)

Convert between types by calling the type like a function:

| Function   | Turns into | Example                  | Result      |
|------------|------------|--------------------------|-------------|
| `int(x)`   | integer    | `int("42")`, `int(3.9)`  | `42`, `3` (truncates) |
| `float(x)` | float      | `float("3.14")`          | `3.14`      |
| `str(x)`   | string     | `str(42)`                | `"42"`      |
| `bool(x)`  | boolean    | `bool(0)`, `bool("a")`   | `False`, `True` |
| `list(x)`  | list       | `list("abc")`            | `['a','b','c']` |

```python
user_input = "30"          # input() always gives a string
age = int(user_input) + 1  # convert before doing maths
print(age)                 # 31
```

> **Watch out:** `int("3.9")` raises a `ValueError` — `int()` won't parse a string that looks like a
> float. Do `int(float("3.9"))` instead, which gives `3`. Also note `int(3.9)` truncates toward zero
> (gives `3`), it does **not** round.

---

## Object identity: `is` vs `==`

- `==` asks: **do these have the same value?**
- `is` asks: **are these the literally same object in memory?**

```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)   # True  — same contents
print(a is b)   # False — two separate list objects
print(id(a), id(b))  # different memory addresses
```

> **Watch out — small-integer caching:** CPython pre-creates and reuses the small integers from
> roughly `-5` to `256`, so two variables holding the same small int share one object — `a = 256` and
> `b = 256` gives `a is b == True` everywhere. Larger ints like `257` are **not** cached, and whether
> `a is b` is `True` or `False` then depends on context: two `257` literals in the *same* script,
> function, or one-liner get folded into a single constant (`True`), but two `257`s entered as
> *separate* lines in the `>>>` shell, or a literal versus a computed `int("257")`, are different
> objects (`False`). The point isn't the exact rule — it's that identity for equal numbers is an
> unreliable implementation detail. *Never* use `is` to compare values; use `==`, and reserve `is`
> for `None`, `True`, and `False`.

---

## Multiple assignment & swapping

```python
x, y, z = 1, 2, 3      # assign several at once
a = b = c = 0          # same value to several names
x, y = y, x            # swap without a temp variable — very Pythonic
```

---

## Quick recap

- A variable is a name bound to a value; the *value* has a type, the *name* doesn't.
- Names: `snake_case`, descriptive, can't start with a digit or be a keyword.
- Core types: `int`, `float`, `complex`, `bool`, `str`, `list`, `tuple`, `dict`, `set`, `None`.
- `bool` is a subclass of `int` (`True == 1`).
- Immutable: numbers, `str`, `tuple`, `bool`, `frozenset`. Mutable: `list`, `dict`, `set`.
- Convert with `int()`, `float()`, `str()`, `bool()`, etc.
- `==` compares value; `is` compares identity. Use `is` only for `None`/`True`/`False`.

---

## Practice questions

Try every one before opening
[`solutions/02-variables-and-data-types-solutions.md`](../solutions/02-variables-and-data-types-solutions.md).

1. What does "dynamically typed" mean? Give a two-line code example.
2. Is `2name = 5` valid? Why or why not?
3. Are `total` and `Total` the same variable? What feature of Python decides this?
4. Which naming style does PEP 8 recommend for ordinary variables?
5. How do you signal to other programmers that a value is a constant?
6. Does Python *enforce* constants? Explain.
7. List Python's three numeric types with an example of each.
8. What is the output of `type(3.0)`?
9. What is the difference between `type()` and `isinstance()`, and which should you use in real code?
10. Predict and explain: `isinstance(True, int)`.
11. Predict and explain: `True + True + True`.
12. Why does `int` not overflow in Python? What does `2 ** 100` return — a number or an error?
13. Write `1000000` in a more readable way using a Python 3.6+ feature.
14. What type is `None`, and how many `None` objects exist?
15. Why should you write `x is None` instead of `x == None`?
16. List four falsy values in Python.
17. Predict the output:
    ```python
    if "0":
        print("yes")
    else:
        print("no")
    ```
18. What does `bool([])` return, and why?
19. Convert the string `"42"` to an integer and add 8.
20. What happens when you run `int("3.9")`? How do you correctly get `3` from that string?
21. Does `int(3.9)` round or truncate? What is the result?
22. Convert the integer `100` to a string and explain one reason you'd need to.
23. What does `list("cat")` produce?
24. Explain the difference between `==` and `is`.
25. Predict and explain:
    ```python
    a = [1, 2]
    b = [1, 2]
    print(a == b, a is b)
    ```
26. What is the small-integer caching behaviour in CPython, and why must you never rely on it?
27. Which built-in types are immutable? Name at least four.
28. Which built-in types are mutable? Name at least three.
29. Swap the values of `a` and `b` in a single line without a temporary variable.
30. After `x = y = []`, you run `x.append(1)`. What does `y` now contain, and why?
