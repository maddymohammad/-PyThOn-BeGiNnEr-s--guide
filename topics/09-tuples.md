# 09 · Tuples

> **You will be able to:** create and unpack tuples, explain how they differ from lists, and know
> when their immutability makes them the right choice.

---

## What is a tuple?

A tuple is an **ordered, immutable** sequence. Think of it as a list you can't change after creating
it. That immutability is the whole point — it signals "this group of values belongs together and
won't be modified."

```python
point = (3, 4)
rgb = (255, 0, 127)
mixed = (1, "two", 3.0)
empty = ()
```

---

## Creating tuples — and the one-element trap

It's the **comma** that makes a tuple, not the parentheses:

```python
single = (5,)     # a one-element tuple
not_a_tuple = (5) # just the integer 5 — the parentheses only group
print(type(single))      # <class 'tuple'>
print(type(not_a_tuple)) # <class 'int'>
```

You can even omit the parentheses entirely (this is called **tuple packing**):

```python
t = 1, 2, 3        # (1, 2, 3)
```

| You write     | You get                        |
|---------------|--------------------------------|
| `()`          | empty tuple                    |
| `(5)`         | the integer `5` (not a tuple!) |
| `(5,)`        | one-element tuple `(5,)`       |
| `1, 2, 3`     | tuple `(1, 2, 3)`              |
| `tuple("ab")` | `('a', 'b')`                   |

> **Watch out:** The single most common tuple bug is forgetting the trailing comma. `(5)` is an
> integer; `(5,)` is a tuple.

---

## Indexing and slicing

Exactly like lists and strings — but read-only:

```python
t = (10, 20, 30, 40)
print(t[0])      # 10
print(t[-1])     # 40
print(t[1:3])    # (20, 30)
```

---

## Immutability (with a twist)

You cannot reassign, add, or remove elements:

```python
t = (1, 2, 3)
t[0] = 99        # TypeError: 'tuple' object does not support item assignment
```

**But** if a tuple *contains* a mutable object, that object can still be changed — the tuple's
reference to it doesn't change, but its contents do:

```python
t = ([1, 2], 3)
t[0].append(9)   # allowed! t is now ([1, 2, 9], 3)
```

> **Watch out:** "Immutable" means the tuple's own slots are fixed, not that everything inside is
> frozen. A tuple of lists still has mutable lists in it.

---

## Unpacking

Assign a tuple's items to multiple variables at once — extremely common and very Pythonic:

```python
point = (3, 4)
x, y = point          # x = 3, y = 4

a, b = b, a           # the swap idiom is really tuple packing + unpacking
```

Use a starred name to capture "the rest" into a **list**:

```python
first, *rest = (1, 2, 3, 4)              # first = 1, rest = [2, 3, 4]
first, *middle, last = (1, 2, 3, 4, 5)   # first=1, middle=[2,3,4], last=5
```

> **Watch out:** The starred variable collects into a **list**, not a tuple — even when unpacking a
> tuple.

---

## Returning multiple values

Functions return multiple values by packing them into a tuple — you've already seen `divmod`:

```python
def min_max(numbers):
    return min(numbers), max(numbers)   # returns a tuple

low, high = min_max([3, 1, 7])          # unpacks it: low=1, high=7
print(divmod(17, 5))                     # (3, 2)
```

---

## Tuple methods and operations

Because tuples are immutable, they have only two methods: `.count()` and `.index()`. Everything that
doesn't modify works:

```python
t = (1, 2, 2, 3)
print(t.count(2))    # 2
print(t.index(3))    # 3  -> position of first 3
print(len(t))        # 4
print(2 in t)        # True
print((1, 2) + (3,)) # (1, 2, 3)   concatenation
print((0,) * 3)      # (0, 0, 0)   repetition
```

---

## Tuples as dictionary keys

Because tuples are immutable (hashable), they can be used as dictionary keys or set elements — **lists
cannot**:

```python
locations = {(40.7, -74.0): "New York"}   # works
# {[40.7, -74.0]: "NYC"}                   # TypeError: unhashable type: 'list'
```

This is only true if every element of the tuple is itself hashable.

---

## List or tuple — which?

| Use a **list** when…                       | Use a **tuple** when…                          |
|--------------------------------------------|------------------------------------------------|
| the collection will change (add/remove)    | the collection is fixed                        |
| items are the "same kind" of thing         | items form a fixed record (e.g. a coordinate)  |
| you need methods like `sort`, `append`     | you need a dict key or set element             |
| —                                          | you want to signal "don't modify this"         |

---

## Quick recap

- Tuples are **ordered and immutable**; the **comma** makes the tuple (`(5,)` not `(5)`).
- You can pack (`t = 1, 2, 3`) and unpack (`x, y = t`); `*rest` collects extras into a **list**.
- Items can't be reassigned, but mutable items *inside* a tuple can still change.
- Only two methods: `.count()` and `.index()`; `+`, `*`, `in`, `len()`, slicing all work.
- Functions return multiple values as tuples.
- Tuples can be dict keys / set members (if all elements are hashable); lists cannot.

---

## Practice questions

Try every one before opening
[`solutions/09-tuples-solutions.md`](../solutions/09-tuples-solutions.md).

1. What two properties define a tuple?
2. What makes a tuple a tuple — the parentheses or the comma? Prove it with `(5)` vs `(5,)`.
3. What is the type of `(5)`? What is the type of `(5,)`?
4. Write a tuple three different ways: with parentheses, without parentheses, and from a string.
5. How do you create an empty tuple?
6. For `t = (10, 20, 30, 40)`, what are `t[0]`, `t[-1]`, and `t[1:3]`?
7. What happens when you run `t[0] = 99` on a tuple? Why?
8. Predict and explain:
    ```python
    t = ([1, 2], 3)
    t[0].append(9)
    print(t)
    ```
9. Why is the example in question 8 allowed even though tuples are immutable?
10. Unpack `(3, 4)` into variables `x` and `y`.
11. What is the connection between tuple unpacking and the `a, b = b, a` swap?
12. Predict the values: `first, *rest = (1, 2, 3, 4)`.
13. Is `rest` in the previous question a tuple or a list?
14. Predict: `first, *middle, last = (1, 2, 3, 4, 5)`.
15. How does a function return more than one value?
16. What does `divmod(17, 5)` return, and what type is it?
17. Write a function that returns both the minimum and maximum of a list, then unpack the result.
18. Why do tuples have only two methods? Name them.
19. What does `(1, 2, 2, 3).count(2)` return?
20. What does `(1, 2, 3).index(2)` return?
21. What is `(1, 2) + (3,)`? What is `(0,) * 3`?
22. Can a tuple be used as a dictionary key? Can a list? Explain why.
23. What condition must hold for a tuple to be usable as a dict key?
24. Give two situations where you'd choose a tuple over a list.
25. Give two situations where a list is the better choice.
26. Does `len()` work on a tuple? Does `in`?
27. Can you sort a tuple in place with a `.sort()` method? What can you do instead?
28. Predict and explain: `x = (5); print(x + 1)`.
29. What's the result of trying to use `[1, 2]` as a dictionary key, and what's the error?
30. Convert the tuple `(1, 2, 3)` into a list, add `4`, then convert it back to a tuple.
