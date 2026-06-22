# 11 · Sets

> **You will be able to:** use sets to handle uniqueness, perform set maths (union, intersection,
> difference), and know why membership tests on a set are so fast.

---

## What is a set?

A set is an **unordered** collection of **unique**, hashable elements. It's mutable, but it can't
contain duplicates, and it doesn't track position.

```python
colours = {"red", "green", "blue"}
numbers = {1, 2, 3}
```

Two things make sets special: they automatically drop duplicates, and checking membership (`x in s`)
is very fast — on average it doesn't slow down as the set grows, unlike a list.

---

## Creating sets — and the empty-set trap

```python
s = {1, 2, 3}
from_list = set([1, 1, 2, 3])   # {1, 2, 3} -> duplicates removed
empty = set()                   # the ONLY way to make an empty set
```

> **Watch out:** `{}` is an empty **dictionary**, not a set. For an empty set you must write `set()`.

```python
print(type({}))      # <class 'dict'>
print(type(set()))   # <class 'set'>
```

---

## Uniqueness: the killer feature

Adding a duplicate does nothing, which makes sets the standard tool for de-duplicating:

```python
nums = [1, 1, 2, 3, 3, 3]
unique = set(nums)          # {1, 2, 3}
unique_list = list(set(nums))   # back to a list (order not guaranteed)
```

---

## Unordered: no indexing

Because sets have no order, you cannot index or slice them:

```python
s = {1, 2, 3}
s[0]        # TypeError: 'set' object is not subscriptable
```

> **Watch out:** Don't rely on the order items print in. Small integer sets often *appear* sorted,
> but that's an implementation accident — set order is not guaranteed.

---

## Adding and removing

| Method          | Effect                                                   |
|-----------------|----------------------------------------------------------|
| `.add(x)`       | Add an element (no effect if already present)            |
| `.remove(x)`    | Remove `x` — raises `KeyError` if it's not there         |
| `.discard(x)`   | Remove `x` if present — **no error** if it's not there   |
| `.pop()`        | Remove and return an **arbitrary** element               |
| `.clear()`      | Remove everything                                        |

```python
s = {1, 2, 3}
s.add(4)        # {1, 2, 3, 4}
s.discard(9)    # no error, even though 9 isn't there
s.remove(9)     # KeyError!
```

> **Watch out:** `.remove()` errors on a missing element; `.discard()` is the safe version. And
> `.pop()` removes some *arbitrary* element, not "the first."

---

## Set maths

This is where sets shine. Each operation has both an operator and a method.

| Operation              | Operator | Method                     | `{1,2,3}` ◦ `{2,3,4}` |
|------------------------|----------|----------------------------|------------------------|
| Union (all elements)   | `\|`     | `.union()`                 | `{1, 2, 3, 4}`         |
| Intersection (in both) | `&`      | `.intersection()`          | `{2, 3}`               |
| Difference (in first only) | `-`  | `.difference()`            | `{1}`                  |
| Symmetric difference (in exactly one) | `^` | `.symmetric_difference()` | `{1, 4}`     |

```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a | b)   # {1, 2, 3, 4}
print(a & b)   # {2, 3}
print(a - b)   # {1}
print(a ^ b)   # {1, 4}
```

### Subset / superset / disjoint

```python
print({1, 2} <= {1, 2, 3})          # True  -> is subset
print({1, 2, 3} >= {1, 2})          # True  -> is superset
print({1, 2}.isdisjoint({3, 4}))    # True  -> no elements in common
```

---

## Membership and length

```python
s = {1, 2, 3}
print(2 in s)      # True  — fast, average O(1)
print(len(s))      # 3
```

Checking `x in s` on a large set is dramatically faster than `x in big_list`, which is the main reason
to convert a list to a set when you'll do many membership tests.

---

## Elements must be hashable

Like dict keys, set elements must be hashable — so no lists inside a set:

```python
{1, 2, (3, 4)}     # fine — tuples are hashable
{1, [2, 3]}        # TypeError: unhashable type: 'list'
```

A **`frozenset`** is an immutable set; because it's hashable, it can itself be an element of another
set or a dictionary key.

---

## Set comprehensions

Same shape as a list comprehension, with braces — duplicates collapse automatically:

```python
evens = {x * 2 for x in range(5)}    # {0, 2, 4, 6, 8}
```

---

## Quick recap

- A set is **unordered**, holds **unique hashable** elements, and is mutable.
- `{}` is an empty dict — use `set()` for an empty set.
- `set(seq)` de-duplicates; `list(set(seq))` removes duplicates from a list (order not guaranteed).
- No indexing or slicing (sets are unordered).
- `.add`, `.discard` (safe), `.remove` (errors if absent), `.pop` (arbitrary element), `.clear`.
- Set maths: union `|`, intersection `&`, difference `-`, symmetric difference `^`.
- `x in s` is fast (average O(1)) — far quicker than scanning a list.
- Elements must be hashable; `frozenset` is the immutable, hashable version.

---

## Practice questions

Try every one before opening
[`solutions/11-sets-solutions.md`](../solutions/11-sets-solutions.md).

1. What three properties describe a set?
2. What are the two standout advantages of a set over a list?
3. How do you create an empty set, and why can't you use `{}`?
4. What is the type of `{}`? What is the type of `set()`?
5. What does `set([1, 1, 2, 3])` produce?
6. Use a set to remove duplicates from the list `[1, 1, 2, 3, 3]`.
7. Why does `s[0]` fail on a set?
8. Should you rely on the order in which set elements print? Explain.
9. What's the difference between `.remove()` and `.discard()`?
10. What does `.pop()` do on a set — and what's surprising about *which* element it removes?
11. Add the element `4` to the set `{1, 2, 3}`.
12. Compute the union of `{1, 2, 3}` and `{2, 3, 4}`.
13. Compute the intersection of `{1, 2, 3}` and `{2, 3, 4}`.
14. Compute the difference `{1, 2, 3} - {2, 3, 4}`.
15. Compute the symmetric difference of `{1, 2, 3}` and `{2, 3, 4}`.
16. In plain words, what does symmetric difference return?
17. Which operator and which method both perform union?
18. Check whether `{1, 2}` is a subset of `{1, 2, 3}`.
19. Check whether `{1, 2, 3}` is a superset of `{1, 2}`.
20. Check whether `{1, 2}` and `{3, 4}` have no elements in common.
21. How do you test whether `2` is in a set, and why is it fast?
22. Roughly how does set membership speed compare to list membership as the collection grows?
23. What does `len()` return for a set?
24. Why does `{1, [2, 3]}` raise an error?
25. What is a `frozenset`, and what can it do that a normal set cannot?
26. Write a set comprehension that produces the doubles of `0`–`4`.
27. Predict: does `{1, 2, 2, 3}` contain a duplicate `2`? What is its length?
28. Given two lists `a` and `b`, find the values that appear in both using sets.
29. Given two lists, find the values in `a` that are **not** in `b` using sets.
30. You need to test membership thousands of times against a big list. What should you do first, and why?
