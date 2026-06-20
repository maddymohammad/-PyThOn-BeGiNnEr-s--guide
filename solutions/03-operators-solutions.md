# 03 · Operators — Solutions

Answers for the 30 questions in [`topics/03-operators.md`](../topics/03-operators.md).

---

**1. `/` vs `//`.**
`/` is true division and always returns a float; `//` is floor division and discards the fractional
part. `7 / 2` → `3.5`; `7 // 2` → `3`.

**2. `%`.**
The remainder after division. `17 % 5` → `2`.

**3. `**` and `^`.**
`**` is exponentiation (power). `2 ^ 3` is **not** `8` because `^` is bitwise XOR, not exponent; it
gives `1`. Use `2 ** 3` for `8`.

**4. `-7 // 2`.**
`-4`. Floor division rounds *down* (toward negative infinity). `-7 / 2` is `-3.5`, and the floor of
`-3.5` is `-4`.

**5. `-7 % 3`.**
`2`. The remainder takes the sign of the divisor (`3`, positive). Check: `(-7 // 3) * 3 + (-7 % 3)`
= `(-3)*3 + 2` = `-9 + 2` = `-7`. ✓

**6. `7 % -3`.**
`-2`. The divisor (`-3`) is negative, so the remainder is negative. Check:
`(7 // -3) * -3 + (7 % -3)` = `(-3)*(-3) + (-2)` = `9 - 2` = `7`. ✓

**7. The identity.**
`a == (a // b) * b + (a % b)` for any valid `a`, `b`.

**8. `divmod(17, 5)`.**
`(3, 2)` — the quotient and remainder together.

**9. `0.1 + 0.2 == 0.3`.**
`False`. Floats are stored in binary, and `0.1`, `0.2`, `0.3` have no exact binary representation, so
`0.1 + 0.2` produces `0.30000000000000004`. This is standard IEEE-754 behaviour, not a Python bug.

**10. Comparing floats correctly.**
```python
import math
math.isclose(0.1 + 0.2, 0.3)   # True
```

**11. Comparison return type.**
`bool` (`True` or `False`).

**12. `5 == 5.0` and `5 is 5.0`.**
`5 == 5.0` → `True` (equal in value). `5 is 5.0` → `False` (an int and a float are different objects;
never use `is` to compare values).

**13. Chained comparison.**
```python
1 <= x <= 100
```

**14. Logical basics.**
`True and False` → `False`; `True or False` → `True`; `not True` → `False`.

**15. Short-circuit.**
Evaluation stops as soon as the outcome is certain. `and` stops at the first falsy operand; `or`
stops at the first truthy one. The right-hand side may never be evaluated.

**16. `0 or "hi"`.**
`"hi"`. `0` is falsy, so `or` moves on and returns the first truthy value, `"hi"`.

**17. `3 and 0`.**
`0`. `3` is truthy, so `and` continues; it returns the first falsy value, `0`.

**18. Fallback.**
```python
name = user or "Guest"
```

**19. Compound assignment.**
```python
total += 5
```

**20. `x //= 3` after `x = 10`.**
`x` becomes `3` (`10 // 3`).

**21. Walrus `:=`.**
It assigns a value to a variable *and* returns that value within the same expression, so you can
assign inside an `if`, `while`, or comprehension. Added in Python 3.8.

**22. `"a" in "cat"`.**
`True`. `in` checks substring membership for strings, and `"cat"` contains `"a"`.

**23. `in` on a dict.**
It checks the **keys**. `"a" in {"a": 1, "b": 2}` is `True`; checking a value would need
`2 in d.values()`.

**24. When to use `is`.**
Only for comparing against the singletons `None`, `True`, and `False` (identity checks). For value
equality, use `==`.

**25. `5 ^ 3`.**
`6`. `^` is bitwise XOR: `101 ^ 011 = 110` = `6`.

**26. `~5`.**
`-6`. The formula is `~x == -x - 1`.

**27. `2 + 3 * 4`.**
`14`. Multiplication has higher precedence than addition, so it's `2 + (3 * 4)` = `2 + 12`.

**28. `2 ** 3 ** 2`.**
`512`. `**` is right-associative, so it evaluates as `2 ** (3 ** 2)` = `2 ** 9` = `512`.

**29. `-2 ** 2`.**
`-4`. `**` binds tighter than the leading unary minus, so it's `-(2 ** 2)`. To get `4`, write
`(-2) ** 2`.

**30. Parenthesise for 20.**
```python
(2 + 3) * 4   # 20
```
