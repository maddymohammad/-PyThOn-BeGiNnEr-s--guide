# 06 · Conditional Statements

> **You will be able to:** make your program take different paths with `if` / `elif` / `else`, write
> compact conditional expressions, and use modern `match`/`case` pattern matching.

---

## The `if` statement

An `if` runs a block **only when its condition is truthy**. The condition is any expression that
evaluates to `True`/`False` (or any truthy/falsy value — see lesson 2).

```python
temperature = 30
if temperature > 25:
    print("It's warm")      # runs only because the condition is True
```

The colon and the indentation are required: everything indented under the `if` is its block.

---

## `if` / `elif` / `else`

Add `elif` ("else if") for more cases and `else` for the fallback. Python checks each condition in
order and runs the **first** block whose condition is true, then skips the rest.

```python
score = 72
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
print(grade)   # C
```

| Keyword | When it runs                                          | How many allowed |
|---------|-------------------------------------------------------|------------------|
| `if`    | its condition is the first true one                   | exactly one (starts the chain) |
| `elif`  | all earlier conditions were false **and** this is true| zero or more     |
| `else`  | every condition above was false                       | zero or one (ends the chain) |

> **Watch out:** Order matters. Because the first true branch wins, put the most specific or
> highest-priority conditions first. If you wrote `score >= 70` before `score >= 90`, an A would be
> labelled C.

### `elif` vs separate `if`s

A chain of `elif`s is **mutually exclusive** — at most one block runs. Several separate `if`s are
**independent** — more than one can run. Use `elif` when the cases are alternatives.

---

## Conditions and truthiness

Conditions use the comparison and logical operators from lesson 3, and any value's truthiness from
lesson 2.

```python
if name and age >= 18:           # both must be truthy
    print("valid adult")

if not items:                    # empty list is falsy
    print("nothing to show")
```

Two style points interviewers notice:

```python
if is_ready == True:   # redundant
if is_ready:           # idiomatic — just use the boolean directly

if len(items) > 0:     # works, but verbose
if items:              # idiomatic — non-empty is truthy
```

> **Watch out — `=` vs `==`:** `=` assigns, `==` compares. Writing `if x = 5:` is a `SyntaxError` in
> Python (which actually saves you from a bug common in other languages). Use `==` to compare.

---

## Chained and combined conditions

```python
if 0 <= score <= 100:            # chained comparison (lesson 3)
    print("valid score")

if day == "Sat" or day == "Sun": # combine with or
    print("weekend")
```

Conditions short-circuit, so it's safe to guard:

```python
if items and items[0] == "x":    # items[0] is only checked if items is non-empty
    ...
```

---

## Nested conditionals and guard clauses

You can put an `if` inside another, but deep nesting gets hard to read. **Guard clauses** — handling
the exceptional case early and returning/continuing — keep code flat:

```python
# Nested (harder to follow)
if user is not None:
    if user.is_active:
        print("welcome")

# Guard style (flatter, clearer)
if user is None:
    print("no user")
elif not user.is_active:
    print("inactive")
else:
    print("welcome")
```

---

## The conditional expression (ternary)

When you just need to pick one of two values, use a one-line conditional expression:

```python
status = "adult" if age >= 18 else "minor"
```

It reads as *value-if-true* `if` *condition* `else` *value-if-false*. Use it for simple choices; for
anything complex, a full `if`/`else` is clearer.

---

## `pass` — the do-nothing placeholder

When the syntax requires a block but you have nothing to put there yet, use `pass`:

```python
if config_missing:
    pass   # TODO: handle this later
```

---

## `match` / `case` (Python 3.10+)

Modern Python offers structural pattern matching — a cleaner alternative to a long `if`/`elif` chain
when you're comparing one value against several constants:

```python
command = "start"
match command:
    case "start":
        print("starting")
    case "stop":
        print("stopping")
    case "pause" | "hold":      # match multiple values with |
        print("pausing")
    case _:                     # _ is the catch-all (like else)
        print("unknown command")
```

> **Watch out:** A bare name in a `case` (like `case x:`) *captures* the value rather than comparing
> to a variable named `x`. To compare against constants, use literals (`case "start":`) or the
> wildcard `_` for the default.

---

## Quick recap

- `if` runs a block when its condition is truthy; `elif` adds alternatives; `else` is the fallback.
- Only the **first** true branch in a chain runs, so order conditions carefully.
- `elif` chains are mutually exclusive; separate `if`s are independent.
- Prefer `if items:` over `if len(items) > 0:` and `if ready:` over `if ready == True:`.
- `=` assigns, `==` compares — `if x = 5:` is a syntax error.
- Ternary: `a if condition else b` for simple two-way choices.
- `pass` fills an empty block; `match`/`case` (3.10+) cleanly handles many constant cases.

---

## Practice questions

Try every one before opening
[`solutions/06-conditionals-solutions.md`](../solutions/06-conditionals-solutions.md).

1. What must follow the condition in an `if` statement, and what defines its block?
2. When does an `else` block run?
3. How many `elif` branches can a single chain have?
4. In an `if`/`elif`/`else` chain, how many blocks run at most?
5. Predict the output:
    ```python
    x = 5
    if x > 0:
        print("positive")
    elif x > 3:
        print("big")
    ```
6. Why does the `elif x > 3` branch above never run for `x = 5`?
7. Rewrite a grade check so an A (`>= 90`) is never mislabelled — what ordering rule applies?
8. What is the difference between three separate `if`s and an `if`/`elif`/`elif` chain?
9. Why is `if is_ready == True:` considered redundant?
10. Rewrite `if len(items) > 0:` the idiomatic way.
11. What happens if you write `if x = 5:`? Why is that arguably helpful?
12. Write a condition that is true only when `name` is non-empty **and** `age` is at least 18.
13. Write a condition that is true when `day` is `"Sat"` or `"Sun"`.
14. Rewrite `0 <= n and n <= 100` as a chained comparison.
15. Why is `if items and items[0] == "x":` safe even when `items` is empty?
16. Convert this to a one-line conditional expression: assign `"even"` if `n % 2 == 0` else `"odd"`.
17. What does the ternary `"yes" if flag else "no"` evaluate to when `flag` is `0`?
18. What is `pass` used for? Give a situation where you'd need it.
19. Rewrite the following with guard clauses to remove the nesting:
    ```python
    if user is not None:
        if user.is_active:
            print("welcome")
    ```
20. From which Python version is `match`/`case` available?
21. Write a `match` statement on `command` that handles `"start"`, `"stop"`, and anything else.
22. How do you match several values in a single `case`?
23. What does `case _:` mean in a `match` block?
24. Why can `case x:` be a trap when you meant to compare against a variable `x`?
25. Predict the output:
    ```python
    n = 0
    if n:
        print("truthy")
    else:
        print("falsy")
    ```
26. Write an `if`/`elif`/`else` that prints `"negative"`, `"zero"`, or `"positive"` for a number `n`.
27. Does the order of branches affect performance and correctness? Explain briefly.
28. What is the result of combining conditions with `and` when the first is `False` — is the second evaluated?
29. Write a single line that sets `fee` to `0` if `is_member` is truthy, otherwise `10`.
30. Rewrite a long `if`/`elif` chain that compares one variable to many string constants using `match`/`case`.
