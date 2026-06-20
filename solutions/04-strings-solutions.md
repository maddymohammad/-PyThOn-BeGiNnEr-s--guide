# 04 · Strings — Solutions

Answers for the 30 questions in [`topics/04-strings.md`](../topics/04-strings.md).

---

**1. Immutable.**
A string can't be changed in place; any "edit" creates a new string. This fails:
```python
s = "cat"
s[0] = "b"   # TypeError: 'str' object does not support item assignment
```
Do `s = "b" + s[1:]` instead.

**2. Three literals.**
Single quotes `'...'`, double quotes `"..."`, and triple quotes `'''...'''` / `"""..."""`. Triple
quotes are useful for text that spans multiple lines and for docstrings.

**3. `s[0]` and `s[-1]`.**
For `"Python"`: `s[0]` → `'P'`, `s[-1]` → `'n'`.

**4. `s[1:4]`.**
`'yth'`. The stop index (`4`) is **exclusive**, so you get indices 1, 2, 3.

**5. Reverse a string.**
```python
s[::-1]
```

**6. `s[::2]`.**
Takes every second character (step of 2), starting from the beginning.

**7. Last three characters.**
```python
s[-3:]
```

**8. `"Age: " + 30`.**
Raises `TypeError` because you can't concatenate a `str` and an `int`. Fixes:
```python
"Age: " + str(30)     # convert
f"Age: {30}"          # f-string (preferred)
```

**9. `len("hello world")`.**
`11` — five letters, a space, five letters.

**10. Concatenate and repeat.**
```python
"a" + "b" + "c"   # 'abc'
"abc" * 3         # 'abcabcabc'
```

**11. As an f-string.**
```python
f"Hi {name}, age {age}"
```

**12. Two decimal places.**
```python
f"{3.14159:.2f}"   # '3.14'
```

**13. Zero-pad to width 4.**
```python
f"{7:04d}"   # '0007'
```

**14. `.find()` vs `.index()` when missing.**
`.find()` returns `-1`; `.index()` raises a `ValueError`.

**15. `"banana".count("a")`.**
`3`.

**16. Strip spaces.**
```python
"  Hello  ".strip()   # 'Hello'
```

**17. Split then join.**
```python
parts = "a,b,c".split(",")   # ['a', 'b', 'c']
" - ".join(parts)            # 'a - b - c'
```

**18. `endswith(".gz")`.**
`True`.

**19. `.capitalize()` vs `.title()`.**
`.capitalize()` upper-cases only the first character and lower-cases the rest;
`.title()` upper-cases the first letter of every word.
```python
"hello world".capitalize()   # 'Hello world'
"hello world".title()        # 'Hello World'
```

**20. Replace `"o"` with `"0"`.**
```python
"foo boo".replace("o", "0")   # 'f00 b00'
```

**21. Only digits.**
```python
"12345".isdigit()   # True
```

**22. Add 1 if numeric.**
```python
value = input("Number: ")
if value.isdigit():
    print(int(value) + 1)
else:
    print("Not a number.")
```

**23. `"PYTHON".lower().capitalize()`.**
Produces `'Python'`. `.lower()` returns `'python'`, then `.capitalize()` returns `'Python'`. Chaining
works because each method returns a new string, which the next method is then called on.

**24. Escapes.**
`\n` is a newline, `\t` is a tab, `\\` is a single literal backslash.

**25. Windows path two ways.**
```python
print("C:\\Users\\Ada")   # escaped backslashes
print(r"C:\Users\Ada")    # raw string
```

**26. `r"\n"`.**
Two characters: a backslash followed by `n`. The `r` prefix disables escape processing, so it is not
a newline.

**27. Membership, case-sensitive.**
`"py" in "python"` → `True`. `"PY" in "python"` → `False`, because `in` is case-sensitive.

**28. Loop over characters.**
```python
for ch in "abc":
    print(ch)
```

**29. `ord` and `chr`.**
`ord("A")` → `65`; `chr(97)` → `'a'`.

**30. Palindrome check.**
```python
word == word[::-1]   # True for "racecar"
```
