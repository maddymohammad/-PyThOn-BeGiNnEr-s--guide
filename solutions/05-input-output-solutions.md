# 05 · Input & Output — Solutions

Answers for the 30 questions in [`topics/05-input-output.md`](../topics/05-input-output.md).

---

**1. `print("a", "b", "c")`.**
Outputs `a b c`. Multiple arguments are joined by the `sep` value, which defaults to a single space.

**2. Comma-separated.**
```python
print("a", "b", "c", sep=", ")   # a, b, c
```

**3. Default `end`.**
A newline, `'\n'`.

**4. `Hi!` on one line.**
```python
print("Hi", end="")
print("!")
```

**5. Blank line.**
```python
print()
```

**6. `input()` return type.**
Always `str`.

**7. `n + n` after typing `5`.**
`"55"`. `n` is the string `"5"`, so `+` concatenates rather than adds.

**8. Make `n` an integer.**
```python
n = int(input("Number: "))
```

**9. Non-numeric input to `int()`.**
A `ValueError`.

**10. Read a price.**
```python
price = float(input("Price: "))
```

**11. `"3 5".split()`.**
`['3', '5']` — split on whitespace into a list of strings.

**12. Two integers on one line.**
```python
a, b = map(int, input().split())
```

**13. Any number of integers into a list.**
```python
nums = list(map(int, input().split()))
```

**14. `map(int, [...])`.**
It applies `int` to each element, producing an iterator that yields `1, 2, 3`. Wrap in `list()` to get
a list.

**15. Two decimals.**
```python
f"{3.14159:.2f}"   # '3.14'
```

**16. Thousands separators.**
```python
f"{1234567:,}"   # '1,234,567'
```

**17. Percentage, one decimal.**
```python
f"{0.25:.1%}"   # '25.0%'
```

**18. Right-align width 8.**
```python
f"{'hi':>8}"   # '      hi'
```

**19. Left-align width 8.**
```python
f"{'hi':<8}"   # 'hi      '
```

**20. Centre width 8.**
```python
f"{'hi':^8}"   # '   hi   '
```

**21. Zero-pad to width 4.**
```python
f"{7:04d}"   # '0007'
```

**22. `f"{255:x}"`.**
`'ff'`. `:x` formats the integer as lowercase hexadecimal.

**23. `f"{255:b}"`.**
`'11111111'` — binary representation.

**24. Predicted output.**
```
A-B-C
```
Each `end="-"` replaces the newline with a dash; the final `print("C")` ends with a normal newline.

**25. `print(1, 2, 3, sep="")`.**
`123` — an empty separator joins them with nothing between.

**26. Output on separate lines.**
Because `print()` adds a newline by default. Set `end=""` to keep successive prints on one line.

**27. `Total: $19.99`.**
```python
print(f"Total: ${total:.2f}")
```

**28. stdout vs stderr.**
stdout is the normal output stream (data/results); stderr is a separate stream for errors and
diagnostics, so they don't get mixed into piped or redirected output.

**29. Print to stderr.**
```python
import sys
print("error", file=sys.stderr)
```

**30. Greet by name.**
```python
name = input("Your name: ")
print(f"Hello, {name}!")
```
