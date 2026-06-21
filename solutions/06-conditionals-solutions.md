# 06 · Conditional Statements — Solutions

Answers for the 30 questions in [`topics/06-conditionals.md`](../topics/06-conditionals.md).

---

**1. After the condition.**
A colon `:`. The indented lines beneath it form the block.

**2. When `else` runs.**
Only when every `if`/`elif` condition above it was false.

**3. Number of `elif`s.**
As many as you like (zero or more).

**4. Blocks that run.**
At most one — the first whose condition is true (or the `else`, if none are).

**5. Predicted output.**
```
positive
```
`x > 0` is true, so that block runs and the rest of the chain is skipped.

**6. Why `elif x > 3` never runs.**
The chain stops at the first true condition. `x > 0` is already true, so no later branch is even
tested.

**7. Ordering rule.**
Check the most specific / highest threshold first (`>= 90` before `>= 80` before `>= 70`). The first
true branch wins, so looser conditions must come last.

**8. Separate `if`s vs a chain.**
Separate `if`s are independent — several can run. An `if`/`elif` chain is mutually exclusive — only
one block runs.

**9. `== True` redundancy.**
`is_ready` is already a boolean, so `if is_ready:` does the same thing. Comparing to `True` adds
nothing and can even be stricter than intended.

**10. Idiomatic non-empty check.**
```python
if items:
    ...
```

**11. `if x = 5:`.**
It's a `SyntaxError` — you can't assign inside an `if`. That's helpful because it prevents the classic
"used `=` when I meant `==`" bug that silently breaks code in some other languages.

**12. Non-empty name and adult.**
```python
if name and age >= 18:
    ...
```

**13. Weekend.**
```python
if day == "Sat" or day == "Sun":
    ...
```

**14. Chained comparison.**
```python
if 0 <= n <= 100:
    ...
```

**15. Safe indexing.**
`and` short-circuits: if `items` is empty (falsy), Python never evaluates `items[0]`, so there's no
`IndexError`.

**16. One-line even/odd.**
```python
label = "even" if n % 2 == 0 else "odd"
```

**17. Ternary with `flag = 0`.**
`"no"`. `0` is falsy, so the `else` value is chosen.

**18. `pass`.**
A do-nothing placeholder for when the syntax requires a block but you have no code yet — for example,
stubbing out a branch or an empty function you'll fill in later.

**19. Guard clauses.**
```python
if user is None:
    return            # or handle the missing case
if not user.is_active:
    return
print("welcome")
```

**20. `match`/`case` version.**
Python 3.10.

**21. `match` on command.**
```python
match command:
    case "start":
        print("starting")
    case "stop":
        print("stopping")
    case _:
        print("unknown")
```

**22. Multiple values in one `case`.**
Separate them with `|`: `case "pause" | "hold":`.

**23. `case _:`.**
The wildcard / catch-all pattern — it matches anything, acting like the `else` of a `match`.

**24. `case x:` trap.**
A bare name in a pattern *captures* (binds) the matched value to that name; it does **not** compare
against an existing variable `x`. It also matches everything, so it behaves like a catch-all.

**25. Predicted output.**
```
falsy
```
`0` is falsy, so the `else` branch runs.

**26. Sign check.**
```python
if n < 0:
    print("negative")
elif n == 0:
    print("zero")
else:
    print("positive")
```

**27. Order, performance, correctness.**
Yes to both. Correctness: the first true branch wins, so wrong ordering gives wrong results.
Performance: conditions are tested top to bottom and testing stops at the first match, so putting
common/cheap cases first can save work.

**28. `and` with a false first operand.**
The second operand is **not** evaluated — `and` short-circuits and returns the first falsy value.

**29. Member fee.**
```python
fee = 0 if is_member else 10
```

**30. Chain → `match`.**
```python
match status:
    case "draft":
        ...
    case "submitted":
        ...
    case "approved":
        ...
    case _:
        ...
```
This is cleaner than a long `if status == "draft": ... elif status == "submitted": ...` chain when
comparing one variable to many constants.
