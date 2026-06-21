# 08 · Lists

> **You will be able to:** build and modify lists, use their methods correctly, write list
> comprehensions, and sidestep the aliasing and copying traps that catch nearly everyone.

---

## What is a list?

A list is an **ordered, mutable** collection. Ordered means items keep their position; mutable means
you can change it in place after creating it. A list can hold items of any type, even mixed:

```python
empty = []
numbers = [1, 2, 3]
mixed = [1, "two", 3.0, True]
from_iterable = list("abc")   # ['a', 'b', 'c']
```

---

## Indexing and slicing

Lists index from `0` (negative from the end) and slice exactly like strings — but because lists are
mutable, you can also *assign* to those positions.

```python
items = ["a", "b", "c", "d"]
print(items[0])     # 'a'
print(items[-1])    # 'd'
print(items[1:3])   # ['b', 'c']  — slicing returns a NEW list
items[0] = "z"      # mutate one item -> ['z', 'b', 'c', 'd']
items[1:3] = ["X"]  # slice assignment -> ['z', 'X', 'd']
```

> **Watch out:** A slice like `items[1:3]` returns a *new* list (a shallow copy of that part). The
> original is unchanged unless you assign back to a slice.

---

## The essential methods

Most list methods **change the list in place and return `None`** — this trips up almost every
beginner.

| Method            | Does                                              | Returns      |
|-------------------|---------------------------------------------------|--------------|
| `.append(x)`      | Add one item to the end                           | `None`       |
| `.extend(iter)`   | Add each item from an iterable to the end         | `None`       |
| `.insert(i, x)`   | Insert `x` at index `i`                            | `None`       |
| `.remove(x)`      | Remove the **first** item equal to `x`            | `None`       |
| `.pop()` / `.pop(i)` | Remove & return the last item (or index `i`)   | the item     |
| `.clear()`        | Remove all items                                  | `None`       |
| `.index(x)`       | Index of the first `x`                            | int (or error)|
| `.count(x)`       | How many times `x` appears                        | int          |
| `.sort()`         | Sort **in place**                                 | `None`       |
| `.reverse()`      | Reverse **in place**                              | `None`       |
| `.copy()`         | Return a shallow copy                             | new list     |

```python
nums = [3, 1, 2]
nums.append(4)        # [3, 1, 2, 4]
nums.sort()           # [1, 2, 3, 4]  (in place)
print(nums.pop())     # 4  -> returns the removed item; nums is [1, 2, 3]
```

> **Watch out — the #1 list mistake:** `.sort()` returns `None`, so `nums = nums.sort()` throws your
> list away and leaves you with `None`. Either call `nums.sort()` on its own line, or use the
> `sorted()` *function*, which returns a new sorted list: `ordered = sorted(nums)`.

### `append` vs `extend`

```python
a = [1, 2]
a.append([3, 4])   # [1, 2, [3, 4]]   — adds the list as ONE element
b = [1, 2]
b.extend([3, 4])   # [1, 2, 3, 4]     — adds each element
```

> **Watch out:** `.remove(x)` raises `ValueError` if `x` isn't present; `.pop(i)` raises `IndexError`
> for a bad index; `.index(x)` raises `ValueError` if not found.

---

## `sort()`/`sorted()` with `reverse` and `key`

```python
words = ["pear", "fig", "banana"]
words.sort(key=len)              # by length -> ['fig', 'pear', 'banana']
nums = sorted([3, 1, 2], reverse=True)   # [3, 2, 1]  (new list)
```

`sorted()` works on any iterable and returns a new list; `.sort()` only exists on lists and mutates.

---

## Operators and built-in functions

```python
[1, 2] + [3, 4]      # [1, 2, 3, 4]   concatenation
[0] * 3              # [0, 0, 0]      repetition
3 in [1, 2, 3]       # True           membership
len([1, 2, 3])       # 3
sum([1, 2, 3])       # 6
min([3, 1, 2])       # 1
max([3, 1, 2])       # 3
```

---

## List comprehensions

A comprehension builds a list from an iterable in one readable expression — the most loved feature in
Python for transforming data.

```python
squares = [n * n for n in range(5)]              # [0, 1, 4, 9, 16]
evens   = [n for n in range(10) if n % 2 == 0]   # [0, 2, 4, 6, 8]
upper   = [w.upper() for w in ["a", "b"]]        # ['A', 'B']
```

The shape is `[expression for item in iterable if condition]`. The `if` part is optional. Prefer a
comprehension over building a list with an empty list plus `.append()` in a loop — it's shorter and
usually faster.

---

## Nested lists (2D)

```python
grid = [[1, 2, 3],
        [4, 5, 6]]
print(grid[0])      # [1, 2, 3]   — first row
print(grid[1][2])   # 6           — row 1, column 2
```

---

## Aliasing and copying — read this twice

Assignment with `=` does **not** copy a list; it makes a second name for the *same* list:

```python
a = [1, 2, 3]
b = a              # b and a point to the SAME list
b.append(4)
print(a)           # [1, 2, 3, 4]  — a changed too!
```

To get an independent list, make a copy:

```python
b = a.copy()       # or a[:] or list(a) — a shallow copy
```

> **Watch out — the multiplication trap:** building a grid with `[[0] * 3] * 3` creates three
> references to the *same* inner list, so editing one row edits them all:
> ```python
> grid = [[0] * 3] * 3
> grid[0][0] = 1
> # grid is now [[1, 0, 0], [1, 0, 0], [1, 0, 0]]  — all rows changed!
> ```
> Build it with a comprehension instead, which makes a fresh inner list each time:
> ```python
> grid = [[0] * 3 for _ in range(3)]
> ```

(A shallow copy duplicates the outer list but still shares nested lists; for fully independent nested
data use `copy.deepcopy()`. You'll meet modules like `copy` in lesson 13.)

---

## Quick recap

- Lists are ordered and **mutable**; index from `0`/`-1`, slice like strings (a slice is a new list).
- Most methods mutate in place and return `None` — `.sort()`, `.reverse()`, `.append()`, etc.
- **Never write `x = x.sort()`**; use `x.sort()` alone, or `sorted(x)` for a new list.
- `.append(x)` adds one item; `.extend(iter)` adds each item.
- `.remove`/`.index` raise `ValueError` if absent; `.pop` raises `IndexError` for bad indices.
- Comprehensions (`[expr for x in it if cond]`) are the idiomatic way to build lists.
- `b = a` aliases the same list; copy with `a.copy()`, `a[:]`, or `list(a)`.
- `[[0]*3]*3` shares one inner list — use `[[0]*3 for _ in range(3)]`.

---

## Practice questions

Try every one before opening
[`solutions/08-lists-solutions.md`](../solutions/08-lists-solutions.md).

1. What two properties define a list? (Hint: order and changeability.)
2. Can a single list hold different types? Give an example.
3. Convert the string `"abc"` into a list of characters.
4. For `items = ["a", "b", "c", "d"]`, what is `items[-1]` and what is `items[1:3]`?
5. Does slicing a list modify the original? What does a slice return?
6. Change the second item of `items` to `"X"` using indexing.
7. What is the difference between `.append(x)` and `.extend(x)`? Show both on `[1, 2]` with `[3, 4]`.
8. What does `.pop()` return, and how does it differ from `.remove()`?
9. What error does `[1, 2].remove(9)` raise?
10. Predict and explain: `result = [3, 1, 2].sort()`. What is `result`?
11. Sort `[3, 1, 2]` into a **new** list without changing the original.
12. Sort `["pear", "fig", "banana"]` by word length.
13. Sort `[1, 2, 3]` in descending order.
14. What does `[1, 2] + [3, 4]` produce? What about `[0] * 3`?
15. How do you check whether `5` is in a list?
16. What do `len`, `sum`, `min`, and `max` return for `[3, 1, 2]`?
17. Write a list comprehension that produces the squares of `0` through `4`.
18. Write a comprehension that keeps only the even numbers from `range(10)`.
19. Why is a comprehension usually preferred over an empty list plus `.append()` in a loop?
20. For `grid = [[1, 2, 3], [4, 5, 6]]`, how do you access the value `6`?
21. Predict and explain:
    ```python
    a = [1, 2, 3]
    b = a
    b.append(4)
    print(a)
    ```
22. How do you make `b` an independent copy of list `a`? Give two ways.
23. Predict and explain:
    ```python
    grid = [[0] * 3] * 3
    grid[0][0] = 1
    print(grid)
    ```
24. Write the correct way to build a 3×3 grid of zeros that does **not** share rows.
25. What is the difference between a shallow copy and a deep copy?
26. Insert the value `"x"` at index `1` of `["a", "b", "c"]`.
27. Remove every item from a list, leaving it empty.
28. What does `[1, 2, 2, 3].count(2)` return?
29. Reverse `[1, 2, 3]` in place, then say what the method returned.
30. Given `nums = [1, 2, 3, 4, 5]`, write a comprehension that doubles each odd number and drops the evens.
