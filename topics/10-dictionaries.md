# 10 · Dictionaries

> **You will be able to:** map keys to values, look things up safely, add and remove entries, iterate
> a dictionary, and write dict comprehensions. This is the data structure you'll reach for most.

---

## What is a dictionary?

A dictionary (`dict`) stores data as **key → value** pairs. Keys are unique; each maps to one value.
Dictionaries are **mutable** and, since Python 3.7, keep their **insertion order**.

```python
person = {"name": "Ada", "age": 36, "is_admin": True}
empty = {}
```

Think of it like a real dictionary: you look up a *word* (the key) to get its *definition* (the
value). Lookups are very fast regardless of size.

| Rule about keys                              | Rule about values        |
|----------------------------------------------|--------------------------|
| Must be **unique** (duplicates overwrite)    | Can repeat               |
| Must be **hashable** (str, int, tuple, …)    | Can be any type at all   |
| A list **cannot** be a key                   | A list **can** be a value|

---

## Creating dictionaries

```python
a = {"x": 1, "y": 2}
b = dict(x=1, y=2)                  # keyword form (keys become strings)
c = dict([("x", 1), ("y", 2)])     # from a list of pairs
```

---

## Accessing values

```python
person = {"name": "Ada", "age": 36}
print(person["name"])      # 'Ada'
print(person["email"])     # KeyError: 'email'  -> the key doesn't exist
```

Square brackets raise `KeyError` for a missing key. Use **`.get()`** when a key might be absent — it
returns `None` (or a default you supply) instead of crashing:

```python
print(person.get("email"))          # None
print(person.get("email", "n/a"))   # 'n/a'
```

> **Watch out:** `d["missing"]` raises `KeyError`; `d.get("missing")` returns `None`. Reach for
> `.get()` whenever you're not certain the key exists.

---

## Adding and updating

The same syntax both adds a new pair and updates an existing one:

```python
person["age"] = 37        # update existing key
person["city"] = "London" # add new key
```

Because keys are unique, assigning to an existing key overwrites its value:

```python
d = {"a": 1}
d["a"] = 2
print(d)        # {'a': 2}
```

---

## Removing entries

| Way               | Effect                                                  |
|-------------------|---------------------------------------------------------|
| `del d[key]`      | Remove the pair (raises `KeyError` if absent)           |
| `d.pop(key)`      | Remove and **return** the value (`KeyError` if absent)  |
| `d.pop(key, def)` | Remove and return, or return `def` if absent (no error) |
| `d.popitem()`     | Remove and return the **last** inserted `(key, value)`  |
| `d.clear()`       | Remove everything                                       |

```python
person = {"name": "Ada", "age": 36}
age = person.pop("age")    # age = 36; person is now {'name': 'Ada'}
```

---

## The view methods: keys, values, items

```python
prices = {"apple": 50, "banana": 20}
print(prices.keys())     # dict_keys(['apple', 'banana'])
print(prices.values())   # dict_values([50, 20])
print(prices.items())    # dict_items([('apple', 50), ('banana', 20)])
```

These return **view objects** that stay in sync with the dict. Wrap one in `list()` if you need a
static list:

```python
list(prices.keys())      # ['apple', 'banana']
```

---

## Iterating a dictionary

```python
prices = {"apple": 50, "banana": 20}

for key in prices:                 # iterating a dict yields its KEYS
    print(key)

for key, value in prices.items():  # the usual way — keys and values together
    print(f"{key}: {value}")

for value in prices.values():      # just the values
    print(value)
```

> **Watch out:** Don't add or remove keys *while* iterating a dictionary — it raises a
> `RuntimeError`. Iterate over `list(d.keys())` if you need to modify during the loop.

---

## Membership and length

```python
prices = {"apple": 50, "banana": 20}
print("apple" in prices)       # True   -> 'in' checks KEYS
print(50 in prices)            # False  -> not a key (it's a value)
print(50 in prices.values())   # True
print(len(prices))             # 2
```

---

## Merging dictionaries

```python
a = {"x": 1, "y": 2}
b = {"y": 99, "z": 3}

a.update(b)            # mutates a -> {'x': 1, 'y': 99, 'z': 3}
merged = {**a, **b}    # new dict via unpacking
merged2 = a | b        # the merge operator (Python 3.9+)
```

When keys collide, the **right-hand** dict wins.

---

## `setdefault` — get-or-insert

`setdefault(key, default)` returns the value if the key exists, otherwise inserts the key with
`default` and returns it. It's handy for grouping:

```python
groups = {}
for name in ["Ann", "Al", "Bob"]:
    groups.setdefault(name[0], []).append(name)
# {'A': ['Ann', 'Al'], 'B': ['Bob']}
```

(For counting and grouping, the `collections` module's `Counter` and `defaultdict` are even cleaner —
you'll meet modules in lesson 13.)

---

## Dictionary comprehensions

Build a dict from an iterable in one expression:

```python
squares = {n: n * n for n in range(5)}     # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
prices = {"apple": 50, "banana": 20}
cheap  = {k: v for k, v in prices.items() if v < 30}   # {'banana': 20}
```

---

## Quick recap

- A dict maps **unique, hashable keys** to values; it's mutable and keeps insertion order (3.7+).
- `d[key]` raises `KeyError` if missing; `d.get(key, default)` is the safe lookup.
- `d[key] = value` both adds and updates; assigning an existing key overwrites it.
- Remove with `del`, `.pop()`, `.popitem()`, or `.clear()`.
- `.keys()`, `.values()`, `.items()` return live views — wrap in `list()` for a snapshot.
- `in` and iteration default to **keys**; use `.items()` for pairs, `.values()` for values.
- Merge with `.update()`, `{**a, **b}`, or `a | b` (3.9+); on conflicts the right side wins.
- Comprehensions: `{k: v for ... if ...}`.

---

## Practice questions

Try every one before opening
[`solutions/10-dictionaries-solutions.md`](../solutions/10-dictionaries-solutions.md).

1. What does a dictionary store, and what are its two halves called?
2. Are dictionaries ordered? Since which Python version?
3. What two rules must dictionary **keys** obey?
4. Can a value repeat across different keys? Can a key repeat?
5. Why can't a list be a dictionary key, but a tuple can?
6. Create the same two-entry dict in two different ways.
7. What does `person["email"]` do if `"email"` isn't a key?
8. Rewrite that lookup so it returns `None` instead of crashing.
9. How do you make a missing-key lookup return the string `"unknown"` as a default?
10. Write the line that adds a new key `"city"` with value `"London"` to `person`.
11. What happens when you assign to a key that already exists?
12. Predict the output:
    ```python
    d = {"a": 1}
    d["a"] = 2
    print(d)
    ```
13. Name three ways to remove an entry, and how `del` differs from `.pop()`.
14. What does `.pop("age")` return, and what's left in the dict afterward?
15. What does `.popitem()` remove and return?
16. What do `.keys()`, `.values()`, and `.items()` return — and why "view"?
17. How do you turn `d.keys()` into an actual list?
18. When you write `for k in d:`, are you iterating keys or values?
19. Write a loop that prints `"key: value"` for every pair in a dict.
20. Why is it unsafe to add keys to a dict while iterating it, and what's the fix?
21. Does `"apple" in prices` check keys or values?
22. How do you check whether the value `50` exists in a dict?
23. What does `len()` return for a dictionary?
24. Merge `{"x": 1, "y": 2}` and `{"y": 9, "z": 3}` two different ways.
25. When two dicts being merged share a key, which value wins?
26. What does `setdefault("A", [])` do if `"A"` is missing? What if it's present?
27. Write a dict comprehension mapping each number `0`–`4` to its square.
28. Write a dict comprehension that keeps only the entries of `prices` whose value is under 30.
29. Predict and explain: `{"a": 1, "a": 2}`.
30. Given `votes = ["yes", "no", "yes", "yes"]`, build a dict counting each option using `.get()`.
