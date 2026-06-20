# 04 · Strings

> **You will be able to:** create strings, index and slice them, search and transform them, and
> format them cleanly with f-strings — the skills you'll use in almost every program you write.

---

## What is a string?

A string (`str`) is an **ordered, immutable** sequence of characters. "Immutable" means once created
it cannot be changed in place — every "edit" actually produces a *new* string.

```python
single = 'hello'
double = "hello"          # single and double quotes are interchangeable
multi = """spans
multiple lines"""         # triple quotes preserve line breaks
```

Use double quotes when the text contains an apostrophe (`"it's"`) and single quotes when it contains
double quotes (`'she said "hi"'`) — that way you avoid escaping.

---

## Indexing and slicing

Each character has a position. Indexing starts at **0**; negative indices count from the end.

```
 H  e  l  l  o
 0  1  2  3  4     (forward)
-5 -4 -3 -2 -1     (backward)
```

```python
s = "Hello"
print(s[0])     # 'H'  (first)
print(s[-1])    # 'o'  (last)
print(s[1:4])   # 'ell' (slice: start inclusive, stop EXCLUSIVE)
print(s[:2])    # 'He'  (from start)
print(s[2:])    # 'llo' (to end)
print(s[::-1])  # 'olleH' (reverse, using a step of -1)
```

Slice syntax is `s[start:stop:step]`. All three parts are optional.

| Expression | Meaning                          | On `"Hello"` |
|------------|----------------------------------|--------------|
| `s[0]`     | First character                  | `'H'`        |
| `s[-1]`    | Last character                   | `'o'`        |
| `s[1:4]`   | Index 1 up to (not incl.) 4      | `'ell'`      |
| `s[:3]`    | First three characters           | `'Hel'`      |
| `s[2:]`    | From index 2 to the end          | `'llo'`      |
| `s[::2]`   | Every second character           | `'Hlo'`      |
| `s[::-1]`  | Whole string reversed            | `'olleH'`    |

> **Watch out:** Strings are immutable, so `s[0] = "J"` raises a `TypeError`. To "change" a character,
> build a new string: `"J" + s[1:]`.

---

## Combining and repeating

```python
greeting = "Hi" + ", " + "Ada"   # concatenation -> 'Hi, Ada'
line = "-" * 20                   # repetition -> 20 dashes
print(len(greeting))              # 7 -> length in characters
```

> **Watch out:** You cannot concatenate a string and a number directly. `"Age: " + 30` raises a
> `TypeError`. Convert first (`"Age: " + str(30)`) or, better, use an f-string.

---

## Formatting strings

There are three ways; **f-strings are the modern default** (Python 3.6+).

| Style       | Example                                  | Notes                       |
|-------------|------------------------------------------|-----------------------------|
| f-string    | `f"Hi {name}, you are {age}"`            | Preferred — readable & fast |
| `.format()` | `"Hi {}, you are {}".format(name, age)`  | Older, still common         |
| `%` (printf)| `"Hi %s, you are %d" % (name, age)`      | Legacy; avoid in new code   |

f-strings can hold any expression and support format specifiers:

```python
name, score = "Ada", 92.567
print(f"{name} scored {score:.1f}")     # Ada scored 92.6   (.1f = 1 decimal place)
print(f"{42:05d}")                       # 00042             (pad to width 5 with zeros)
print(f"{0.25:.0%}")                     # 25%               (percentage)
print(f"{name!r}")                       # 'Ada'             (!r shows the repr, with quotes)
```

---

## Common string methods

Strings come with a rich toolbox. Because strings are immutable, **every method returns a new
string** — it never modifies the original.

| Method                     | Does                                   | Example → Result                       |
|----------------------------|----------------------------------------|----------------------------------------|
| `.upper()` / `.lower()`    | Change case                            | `"Hi".upper()` → `'HI'`                |
| `.strip()`                 | Remove leading/trailing whitespace     | `"  hi  ".strip()` → `'hi'`            |
| `.lstrip()` / `.rstrip()`  | Strip one side only                    | `"  hi".lstrip()` → `'hi'`             |
| `.replace(a, b)`           | Replace all `a` with `b`               | `"aaa".replace("a","b")` → `'bbb'`     |
| `.split(sep)`              | Split into a list                      | `"a,b".split(",")` → `['a','b']`       |
| `sep.join(list)`           | Join a list into a string              | `",".join(["a","b"])` → `'a,b'`        |
| `.find(sub)`               | Index of `sub`, or `-1` if absent      | `"cat".find("z")` → `-1`               |
| `.index(sub)`              | Index of `sub`, or **error** if absent | `"cat".index("a")` → `1`               |
| `.count(sub)`              | How many times `sub` appears           | `"banana".count("a")` → `3`            |
| `.startswith()` / `.endswith()` | Test the ends                     | `"file.py".endswith(".py")` → `True`   |
| `.capitalize()`            | First letter upper, rest lower         | `"hELLO".capitalize()` → `'Hello'`     |
| `.title()`                 | Capitalise each word                   | `"hi there".title()` → `'Hi There'`    |
| `.zfill(n)`                | Pad with leading zeros to width `n`    | `"42".zfill(5)` → `'00042'`            |

> **Watch out:** `.find()` returns `-1` when the substring isn't there; `.index()` raises a
> `ValueError`. Use `.find()` when "not found" is normal, `.index()` when it should never happen.

### The `is...` test methods

These return booleans and are handy for validating input:

| Method        | True when the string…                  | Example                      |
|---------------|----------------------------------------|------------------------------|
| `.isdigit()`  | contains only digits                   | `"123".isdigit()` → `True`   |
| `.isalpha()`  | contains only letters                  | `"abc".isalpha()` → `True`   |
| `.isalnum()`  | contains only letters/digits           | `"a1".isalnum()` → `True`    |
| `.isspace()`  | contains only whitespace               | `"  ".isspace()` → `True`    |
| `.islower()`  | is all lowercase                       | `"abc".islower()` → `True`   |

```python
age = input("Age: ")
if age.isdigit():
    print(int(age) + 1)
else:
    print("Please enter a number.")
```

---

## Escape sequences and raw strings

A backslash starts a special sequence:

| Sequence | Means            |
|----------|------------------|
| `\n`     | New line         |
| `\t`     | Tab              |
| `\\`     | A literal backslash |
| `\'`     | A literal single quote |
| `\"`     | A literal double quote |

```python
print("Line 1\nLine 2")     # prints on two lines
print("C:\\Users\\Ada")     # C:\Users\Ada
```

A **raw string** (`r"..."`) turns off escaping — useful for Windows paths and regular expressions:

```python
print(r"C:\Users\Ada")      # C:\Users\Ada  (the \U is taken literally)
```

---

## Membership and iteration

```python
print("py" in "python")     # True
print("z" not in "python")  # True

for ch in "abc":            # strings are iterable
    print(ch)               # a, then b, then c
```

`ord()` and `chr()` convert between a character and its code point:

```python
print(ord("A"))   # 65
print(chr(97))    # 'a'
```

---

## Quick recap

- Strings are **ordered and immutable** sequences of characters.
- Index from `0` (or `-1` from the end); slice with `s[start:stop:step]`; `s[::-1]` reverses.
- `+` concatenates, `*` repeats, `len()` measures; you must `str()`-convert numbers to join them.
- Prefer **f-strings**; use format specifiers like `:.2f`, `:05d`, `:.0%`.
- Methods return *new* strings: `.upper`, `.strip`, `.replace`, `.split`, `.join`, `.find`, etc.
- `.find()` returns `-1` if absent; `.index()` raises an error.
- `\n`, `\t`, `\\` are escapes; `r"..."` disables them.

---

## Practice questions

Try every one before opening
[`solutions/04-strings-solutions.md`](../solutions/04-strings-solutions.md).

1. What does it mean that strings are "immutable"? Give a code example that fails because of it.
2. Name the three ways to write a string literal and when triple quotes are useful.
3. Given `s = "Python"`, what is `s[0]` and what is `s[-1]`?
4. What does `s[1:4]` return for `s = "Python"`? Is the stop index included?
5. How do you reverse a string in one expression?
6. What does `s[::2]` do?
7. How do you get the last three characters of any string `s`?
8. Why does `"Age: " + 30` raise an error, and how do you fix it two ways?
9. What does `len("hello world")` return? (Count carefully.)
10. Concatenate `"a"`, `"b"`, `"c"` and also produce `"abcabcabc"` using an operator.
11. Rewrite `"Hi " + name + ", age " + str(age)` as an f-string.
12. Format `3.14159` to two decimal places using an f-string.
13. Use an f-string to pad the number `7` to width 4 with leading zeros.
14. What is the difference between `.find()` and `.index()` when the substring is missing?
15. What does `"banana".count("a")` return?
16. Convert `"  Hello  "` to `"Hello"` (no surrounding spaces).
17. Split `"a,b,c"` into a list, then join that list back with `" - "`.
18. What does `"file.tar.gz".endswith(".gz")` return?
19. What's the difference between `.capitalize()` and `.title()`? Show each on `"hello world"`.
20. Replace every `"o"` in `"foo boo"` with `"0"`.
21. How do you check if the string `"12345"` contains only digits?
22. Write code that reads input and adds 1 to it only if it is a valid number.
23. What does `"PYTHON".lower().capitalize()` produce, and why does method chaining work?
24. What does `\n` do? What about `\t` and `\\`?
25. Print the Windows path `C:\Users\Ada` two different ways (escaping and raw string).
26. What does `r"\n"` contain — a newline or two characters?
27. Predict and explain: `"py" in "python"` and `"PY" in "python"`.
28. Write a loop that prints each character of `"abc"` on its own line.
29. What do `ord("A")` and `chr(97)` return?
30. Write a one-line check for whether `"racecar"` is a palindrome.
