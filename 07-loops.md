# 07 · Loops

> **You will be able to:** repeat work with `for` and `while`, generate number ranges, control flow
> with `break`/`continue`, and use `enumerate` and `zip` like a pro.

---

## The `for` loop

A `for` loop runs its block once for each item in an **iterable** (a list, string, range, dict, etc.):

```python
for fruit in ["apple", "banana", "cherry"]:
    print(fruit)

for letter in "abc":     # strings are iterable
    print(letter)        # a, b, c
```

The loop variable (`fruit`, `letter`) takes each value in turn. You don't manage an index yourself —
Python hands you the items directly. This is the single biggest difference from loops in many other
languages.

---

## `range()` — generating numbers

`range` produces a sequence of integers on demand. It has up to three parts, and the **stop value is
exclusive**.

| Call                  | Produces            |
|-----------------------|---------------------|
| `range(5)`            | `0, 1, 2, 3, 4`     |
| `range(2, 6)`         | `2, 3, 4, 5`        |
| `range(0, 10, 2)`     | `0, 2, 4, 6, 8`     |
| `range(5, 0, -1)`     | `5, 4, 3, 2, 1`     |

```python
for i in range(5):
    print(i)        # 0 1 2 3 4 — five iterations
```

> **Watch out:** `range(5)` stops *before* 5, giving 0–4 (five numbers). Forgetting the exclusive
> stop is the most common off-by-one error.

---

## The `while` loop

A `while` loop repeats **as long as its condition stays true**. You're responsible for changing
something so the loop eventually ends.

```python
count = 3
while count > 0:
    print(count)
    count -= 1      # without this line, the loop never stops
print("Lift off!")
```

> **Watch out:** If the condition never becomes false, you get an **infinite loop**. The usual cause
> is forgetting to update the variable the condition depends on. (Press `Ctrl+C` to stop a runaway
> program.)

**Rule of thumb:** use `for` when you know the items or the number of repetitions; use `while` when
you loop until some condition changes.

---

## `break` and `continue`

| Statement  | Effect                                                        |
|------------|---------------------------------------------------------------|
| `break`    | Exit the loop immediately                                     |
| `continue` | Skip the rest of this iteration and jump to the next one      |

```python
for n in range(10):
    if n == 5:
        break        # stop entirely at 5
    print(n)         # 0 1 2 3 4

for n in range(5):
    if n % 2 == 0:
        continue     # skip even numbers
    print(n)         # 1 3
```

---

## The loop `else` clause

Both `for` and `while` can have an `else` block. It runs **only if the loop finished normally** (i.e.
was *not* ended by `break`). This is a genuine interview favourite because it surprises people.

```python
for n in [1, 3, 5]:
    if n % 2 == 0:
        print("found an even number")
        break
else:
    print("no even numbers")   # this runs, because break never fired
```

Read it as "if the loop ran to completion without breaking, do the `else`." It's perfect for search
loops.

---

## `enumerate()` — index *and* value

When you need the position as well as the item, use `enumerate` instead of manually tracking an index:

```python
for index, colour in enumerate(["red", "green", "blue"]):
    print(index, colour)        # 0 red / 1 green / 2 blue

for rank, name in enumerate(["Ada", "Linus"], start=1):
    print(rank, name)           # 1 Ada / 2 Linus
```

> **Watch out:** `for i in range(len(items)):` then `items[i]` is a code smell. Prefer iterating the
> items directly, or `enumerate` when you also need the index.

---

## `zip()` — loop over several iterables together

`zip` pairs up items from multiple iterables, stopping at the **shortest** one:

```python
names = ["Ada", "Linus", "Grace"]
ages  = [36, 54, 41]
for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

---

## Iterating dictionaries

```python
prices = {"apple": 50, "banana": 20}

for key in prices:              # iterating a dict yields its KEYS
    print(key)

for key, value in prices.items():   # keys and values together
    print(key, value)

for value in prices.values():       # just the values
    print(value)
```

---

## Nested loops

A loop inside a loop. The inner loop runs fully for each pass of the outer loop:

```python
for row in range(1, 4):
    for col in range(1, 4):
        print(row * col, end="\t")
    print()        # newline after each row
```

---

## A common gotcha: changing a list while looping over it

Removing items from a list *while* iterating it skips elements, because the indices shift under you:

```python
nums = [1, 2, 3, 4]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)   # buggy — skips elements
```

Instead, iterate over a copy, or (better) build a new list with a comprehension:

```python
nums = [n for n in nums if n % 2 != 0]   # safe and clear
```

---

## Quick recap

- `for` iterates the items of an iterable directly; `while` repeats while a condition holds.
- `range(stop)` is exclusive of `stop`; it also takes `start` and `step` (which can be negative).
- `break` exits a loop; `continue` skips to the next iteration.
- A loop's `else` runs only if the loop finished **without** `break`.
- Use `enumerate` for index + value, and `zip` to walk several iterables in parallel.
- Iterating a dict gives keys; use `.items()` / `.values()` for more.
- Never mutate a list while iterating it — build a new one instead.

---

## Practice questions

Try every one before opening
[`solutions/07-loops-solutions.md`](../solutions/07-loops-solutions.md).

1. What is an "iterable"? Give three examples you can loop over.
2. How does a `for` loop in Python differ from a counter-based loop in many other languages?
3. List the numbers produced by `range(5)`.
4. List the numbers produced by `range(2, 6)`.
5. List the numbers produced by `range(0, 10, 2)`.
6. How do you count **down** from 5 to 1 using `range`?
7. Why does `for i in range(5)` run exactly five times and stop at 4?
8. When should you reach for a `while` loop instead of a `for` loop?
9. What is the most common cause of an infinite `while` loop?
10. What does `break` do? What does `continue` do?
11. Predict the output:
    ```python
    for n in range(6):
        if n == 3:
            break
        print(n)
    ```
12. Predict the output:
    ```python
    for n in range(5):
        if n % 2 == 0:
            continue
        print(n)
    ```
13. When does a loop's `else` block run?
14. Predict the output:
    ```python
    for n in [1, 2, 3]:
        if n == 10:
            break
    else:
        print("not found")
    ```
15. Rewrite a search loop using `for`/`else` that prints `"found"` if a list contains `7`, else `"missing"`.
16. What does `enumerate(["a", "b"])` yield on each iteration?
17. How do you make `enumerate` start counting at 1?
18. Why is `for i in range(len(items)): print(items[i])` considered un-Pythonic?
19. What does `zip([1, 2, 3], ["a", "b"])` produce, and how many pairs?
20. Loop over `names` and `scores` in parallel, printing `"name: score"` for each.
21. When you iterate a dictionary directly with `for k in d:`, what do you get — keys or values?
22. How do you loop over both keys and values of a dictionary?
23. Write a nested loop that prints a 3×3 grid of `*` characters.
24. In a nested loop, how many times does the inner block run in total for two 3-iteration loops?
25. What's wrong with removing items from a list while looping over that same list?
26. Show the safe, idiomatic way to keep only the odd numbers from `nums`.
27. Write a `while` loop that prints `1` through `5`.
28. Write a `for` loop that sums the numbers `1` to `100` (use `range`).
29. Print every character of `"hello"` along with its index using `enumerate`.
30. Write a FizzBuzz loop for 1–15: print `"Fizz"` for multiples of 3, `"Buzz"` for 5, `"FizzBuzz"` for both, else the number.
