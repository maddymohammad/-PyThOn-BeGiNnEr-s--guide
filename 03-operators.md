# 03 · Operators

> **You will be able to:** do arithmetic, compare values, combine conditions with boolean logic,
> and avoid the precedence and floating-point traps that catch nearly every beginner.

---

## Arithmetic operators

| Operator | Name             | Example   | Result |
|----------|------------------|-----------|--------|
| `+`      | Addition         | `7 + 2`   | `9`    |
| `-`      | Subtraction      | `7 - 2`   | `5`    |
| `*`      | Multiplication   | `7 * 2`   | `14`   |
| `/`      | Division (true)  | `7 / 2`   | `3.5`  |
| `//`     | Floor division   | `7 // 2`  | `3`    |
| `%`      | Modulo (remainder)| `7 % 2`  | `1`    |
| `**`     | Exponent         | `2 ** 3`  | `8`    |

Two things surprise people immediately:

```python
print(7 / 2)    # 3.5   — / ALWAYS gives a float in Python 3, even for 8 / 2 (4.0)
print(7 // 2)   # 3     — // discards the fractional part
print(2 ** 10)  # 1024  — ** is "to the power of", not "^"
```

> **Watch out:** `^` is **not** exponent in Python — it is bitwise XOR (covered below). Use `**`.

### Floor division and modulo with negatives

This is a favourite interview question because the answers feel wrong at first:

```python
print(-7 // 2)   # -4   floor division rounds toward negative infinity, not toward zero
print(-7 % 3)    #  2   the result of % takes the sign of the DIVISOR
print(7 % -3)    # -2   divisor is negative, so the remainder is negative
```

The rule that ties it together: `a == (a // b) * b + (a % b)` always holds.

`divmod(a, b)` gives both at once:

```python
print(divmod(17, 5))   # (3, 2)  -> quotient 3, remainder 2
```

---

## The float precision trap

```python
print(0.1 + 0.2)            # 0.30000000000000004
print(0.1 + 0.2 == 0.3)     # False  (!)
```

This is **not a Python bug** — it's how binary floating-point works in every language. `0.1` cannot
be represented exactly in binary, so tiny errors accumulate. To compare floats safely:

```python
import math
math.isclose(0.1 + 0.2, 0.3)   # True
```

For money, use the `decimal` module rather than `float`.

---

## Comparison operators

These always return a boolean (`True`/`False`).

| Operator | Meaning                  | Example      | Result  |
|----------|--------------------------|--------------|---------|
| `==`     | Equal to                 | `5 == 5`     | `True`  |
| `!=`     | Not equal to             | `5 != 3`     | `True`  |
| `>`      | Greater than             | `5 > 3`      | `True`  |
| `<`      | Less than                | `5 < 3`      | `False` |
| `>=`     | Greater than or equal    | `5 >= 5`     | `True`  |
| `<=`     | Less than or equal       | `4 <= 3`     | `False` |

```python
print(5 == 5.0)   # True  — equal in value, even though one is int and one is float
print(5 is 5.0)   # False — NOT the same object; never use 'is' to compare values
```

### Chained comparisons

Python lets you chain them the way maths does — most languages can't:

```python
x = 7
print(1 < x < 10)    # True  — reads as (1 < x) and (x < 10)
print(5 < 10 > 3)    # True  — also legal, though usually unclear
```

---

## Logical operators

| Operator | Meaning                              | Example            | Result  |
|----------|--------------------------------------|--------------------|---------|
| `and`    | True only if **both** are true       | `True and False`   | `False` |
| `or`     | True if **at least one** is true     | `True or False`    | `True`  |
| `not`    | Inverts the boolean                  | `not True`         | `False` |

### Short-circuit evaluation (and a subtle return value)

`and`/`or` stop as soon as the result is known, and they return **one of the operands**, not always a
plain `True`/`False`:

```python
print(True and 5)    # 5    — both truthy, so 'and' returns the last value
print(3 and 0)       # 0    — 'and' returns the first falsy value it hits
print(0 or "hi")     # 'hi' — 'or' returns the first truthy value
print("" or "default")  # 'default' — handy for fallback values
```

> **Watch out:** This is why `name = user_input or "Guest"` is a common idiom — if `user_input` is
> empty (falsy), `name` falls back to `"Guest"`.

---

## Assignment operators

| Operator | Equivalent to | Example (start `x = 10`) | Result |
|----------|---------------|--------------------------|--------|
| `=`      | —             | `x = 10`                 | `10`   |
| `+=`     | `x = x + 5`   | `x += 5`                 | `15`   |
| `-=`     | `x = x - 5`   | `x -= 5`                 | `5`    |
| `*=`     | `x = x * 2`   | `x *= 2`                 | `20`   |
| `/=`     | `x = x / 4`   | `x /= 4`                 | `2.5`  |
| `//=`    | `x = x // 3`  | `x //= 3`                | `3`    |
| `%=`     | `x = x % 3`   | `x %= 3`                 | `1`    |
| `**=`    | `x = x ** 2`  | `x **= 2`                | `100`  |

### The walrus operator `:=`

Introduced in Python 3.8, it assigns *and* returns a value in one expression:

```python
if (n := len("hello")) > 3:
    print(f"length is {n}")   # length is 5
```

Use it sparingly — it's handy in loops and comprehensions but can hurt readability if overused.

---

## Membership and identity operators

| Operator | Asks…                                  | Example                  | Result |
|----------|----------------------------------------|--------------------------|--------|
| `in`     | Is this contained in that?             | `"a" in "cat"`           | `True` |
| `not in` | Is this **not** contained in that?     | `3 not in [1, 2]`        | `True` |
| `is`     | Are these the same object in memory?   | `x is None`              | depends |
| `is not` | Are these different objects?           | `x is not None`          | depends |

```python
print("py" in "python")     # True
print(2 in [1, 2, 3])       # True
print("a" in {"a": 1})      # True — for dicts, 'in' checks the KEYS
```

> **Watch out:** Use `is`/`is not` only with `None`, `True`, and `False`. For everything else, use
> `==`/`!=`. (See lesson 02 for why.)

---

## Bitwise operators (briefly)

You will rarely need these as a beginner, but you should recognise them so you don't confuse `^`
with exponent.

| Operator | Name        | Example   | Result |
|----------|-------------|-----------|--------|
| `&`      | AND         | `5 & 3`   | `1`    |
| `\|`     | OR          | `5 \| 3`  | `7`    |
| `^`      | XOR         | `5 ^ 3`   | `6`    |
| `~`      | NOT         | `~5`      | `-6`   |
| `<<`     | Left shift  | `5 << 1`  | `10`   |
| `>>`     | Right shift | `5 >> 1`  | `2`    |

(`~x` equals `-x - 1`; `<<` doubles, `>>` halves, for each shift.)

---

## Operator precedence

When operators mix, Python applies them in a fixed order. From **highest** to **lowest**:

| Tier | Operators                                   |
|------|---------------------------------------------|
| 1    | `()` parentheses                            |
| 2    | `**` (right-associative)                    |
| 3    | unary `+x`, `-x`, `~x`                       |
| 4    | `*`, `/`, `//`, `%`                         |
| 5    | `+`, `-`                                     |
| 6    | `<<`, `>>`                                   |
| 7    | `&` then `^` then `\|`                       |
| 8    | comparisons, `is`, `in` (and their negatives)|
| 9    | `not`                                        |
| 10   | `and`                                        |
| 11   | `or`                                         |

The two precedence traps that show up in interviews:

```python
print(2 + 3 * 4)    # 14, not 20 — * before +
print(2 ** 3 ** 2)  # 512        — ** is right-associative: 2 ** (3 ** 2)
print(-2 ** 2)      # -4         — ** binds tighter than the leading minus: -(2 ** 2)
```

When in doubt, **add parentheses**. Clear beats clever.

---

## Quick recap

- `/` is float division; `//` floors; `%` is remainder; `**` is power.
- Floor division rounds toward −∞; `%` takes the sign of the divisor.
- `0.1 + 0.2 != 0.3` — compare floats with `math.isclose`.
- Comparisons return booleans and can be chained: `1 < x < 10`.
- `and`/`or` short-circuit and return an operand, enabling the `x or default` idiom.
- `^` is XOR, not exponent.
- Precedence: `**` → unary → `* / // %` → `+ -` → comparisons → `not` → `and` → `or`.

---

## Practice questions

Try every one before opening
[`solutions/03-operators-solutions.md`](../solutions/03-operators-solutions.md).

1. What is the difference between `/` and `//`? Give the result of `7 / 2` and `7 // 2`.
2. What does `%` compute? What is `17 % 5`?
3. What does `**` do? Why is `2 ^ 3` not `8`?
4. Predict and explain: `-7 // 2`.
5. Predict and explain: `-7 % 3`.
6. Predict and explain: `7 % -3`.
7. State the identity that relates `//`, `%`, and the original operands.
8. What does `divmod(17, 5)` return?
9. Why does `0.1 + 0.2 == 0.3` evaluate to `False`?
10. Show the correct way to compare `0.1 + 0.2` and `0.3`.
11. What type does a comparison like `5 > 3` return?
12. Predict and explain: `5 == 5.0` and `5 is 5.0`.
13. Rewrite `1 <= x and x <= 100` as a chained comparison.
14. What is the result of `True and False`, `True or False`, and `not True`?
15. What does short-circuit evaluation mean for `and` and `or`?
16. Predict and explain: `0 or "hi"`.
17. Predict and explain: `3 and 0`.
18. Write a one-line fallback so that `name` becomes `user` if it's truthy, otherwise `"Guest"`.
19. Rewrite `total = total + 5` using a compound assignment operator.
20. After `x = 10`, what is `x` following `x //= 3`?
21. What does the walrus operator `:=` do, and in which Python version did it arrive?
22. Predict and explain: `"a" in "cat"`.
23. For a dictionary `{"a": 1, "b": 2}`, does `"a" in d` check keys or values?
24. When is it correct to use `is` instead of `==`?
25. What is `5 ^ 3`, and what operation is `^`?
26. What does `~5` evaluate to, and what's the formula for `~x`?
27. Predict and explain: `2 + 3 * 4`.
28. Predict and explain: `2 ** 3 ** 2`.
29. Predict and explain: `-2 ** 2`. How would you write it to get `4`?
30. Add parentheses to make this evaluate to `20`: `2 + 3 * 4`.
