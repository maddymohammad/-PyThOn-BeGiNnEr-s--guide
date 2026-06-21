# 05 · Input & Output

> **You will be able to:** read input from a user, control exactly how `print()` displays things,
> and format numbers and text cleanly for output.

---

## `print()` in depth

You've used `print()` since lesson 1. It does more than show a single value — it takes any number of
arguments and has options that control the result.

```python
print("Hello", "world")        # Hello world   — args are joined with a space by default
print("a", "b", "c", sep="-")  # a-b-c         — change the separator
print("no newline", end="")    # prints without moving to the next line
print()                        # prints a blank line
```

| Parameter | Default      | Does                                          |
|-----------|--------------|-----------------------------------------------|
| `*args`   | —            | The values to print (as many as you like)     |
| `sep`     | `' '` (space)| What to put *between* multiple values         |
| `end`     | `'\n'` (newline)| What to put *after* the last value         |
| `file`    | stdout       | Where to send output (e.g. `sys.stderr`)      |

```python
print("Loading", end="")
print("...", end="")
print("done")          # Loading...done   (all on one line)
```

> **Watch out:** By default every `print()` ends with a newline. If your output is appearing on
> separate lines when you wanted one line, set `end=""`.

---

## `input()` — reading from the user

`input()` pauses the program, waits for the user to type something and press Enter, and returns what
they typed. **It always returns a string**, even if the user types digits.

```python
name = input("What is your name? ")
print("Hello,", name)
```

The single most common beginner bug lives here:

```python
age = input("Age: ")     # the user types 30
print(age + 1)           # TypeError: can only concatenate str (not "int") to str
```

`age` is the string `"30"`, not the number `30`. Convert it first:

```python
age = int(input("Age: "))   # now age is the integer 30
print(age + 1)              # 31
```

| You want a… | Wrap `input()` in… | Example                          |
|-------------|--------------------|----------------------------------|
| whole number| `int(...)`         | `int(input("Qty: "))`            |
| decimal     | `float(...)`       | `float(input("Price: "))`        |
| text        | nothing            | `input("Name: ")`                |

> **Watch out:** If the user types something that isn't a number, `int(input(...))` raises a
> `ValueError`. You'll learn to handle that gracefully in lesson 15 (Exceptions).

---

## Reading several values at once

Split one line of input on its spaces with `.split()`:

```python
parts = input("Enter two words: ").split()   # "hi there" -> ['hi', 'there']
```

To read several numbers on one line, combine `split()` with `map()`:

```python
a, b = map(int, input("Two numbers: ").split())   # "3 5" -> a=3, b=5
nums = list(map(int, input("Numbers: ").split())) # "1 2 3" -> [1, 2, 3]
```

`map(int, ...)` applies `int` to every piece. (More on `map` later — for now treat this as a recipe.)

---

## Formatting output with f-strings

For anything beyond a plain value, f-strings (lesson 4) are the clean way to build output. The part
after the colon is a **format specifier** that controls width, alignment, decimals, and more.

| Spec        | Meaning                            | Example                | Result          |
|-------------|------------------------------------|------------------------|-----------------|
| `:.2f`      | 2 decimal places (fixed)           | `f"{3.14159:.2f}"`     | `3.14`          |
| `:,`        | thousands separators               | `f"{1234567:,}"`       | `1,234,567`     |
| `:.1%`      | percentage, 1 decimal              | `f"{0.5:.1%}"`         | `50.0%`         |
| `:>10`      | right-align in a width of 10       | `f"{'hi':>10}"`        | `'        hi'`  |
| `:<10`      | left-align in a width of 10        | `f"{'hi':<10}"`        | `'hi        '`  |
| `:^10`      | centre in a width of 10            | `f"{'hi':^10}"`        | `'    hi    '`  |
| `:05d`      | pad an integer to width 5 w/ zeros | `f"{42:05d}"`          | `00042`         |
| `:x` / `:b` | hexadecimal / binary               | `f"{255:x}"`           | `ff`            |

```python
name, total = "Ada", 1234.5
print(f"{name:<10}${total:>10,.2f}")   # Ada       $  1,234.50
```

These specifiers are what let you line columns up neatly in a terminal — handy for tables, receipts,
and reports.

---

## Sending output to standard error

Normal output goes to *stdout*; error or diagnostic messages conventionally go to *stderr*:

```python
import sys
print("Something went wrong", file=sys.stderr)
```

This matters when a program's normal output is being piped somewhere — errors stay separate from data.

---

## Quick recap

- `print()` joins arguments with `sep` (default space) and ends with `end` (default newline).
- `print()` with no arguments prints a blank line; `end=""` keeps output on one line.
- `input()` **always returns a string** — convert with `int()` / `float()` before doing maths.
- `input().split()` reads several values; `map(int, ...)` converts them in one go.
- Format output with f-string specifiers: `:.2f`, `:,`, `:.1%`, `:>10`, `:05d`, `:x`.
- Diagnostic messages can go to `sys.stderr` via `print(..., file=sys.stderr)`.

---

## Practice questions

Try every one before opening
[`solutions/05-input-output-solutions.md`](../solutions/05-input-output-solutions.md).

1. What does `print("a", "b", "c")` output, and why is there a space between the letters?
2. Change the previous call so it prints `a, b, c` (comma and space between each).
3. What is the default value of `print`'s `end` parameter?
4. Write two `print()` calls that together produce `Hi!` on a single line.
5. How do you print a completely blank line?
6. What type does `input()` always return?
7. A user types `5` at `n = input()`. What is `n + n`, and why?
8. Rewrite `n = input("Number: ")` so `n` is usable as an integer.
9. What error do you get from `int(input())` if the user types `hello`?
10. Read a price as a decimal number from the user in one line of code.
11. What does `"3 5".split()` return?
12. Read two integers typed on one line into variables `a` and `b`.
13. Read any number of integers on one line into a list called `nums`.
14. What does `map(int, ["1", "2", "3"])` do conceptually?
15. Format `3.14159` to exactly two decimal places using an f-string.
16. Format the number `1234567` with thousands separators.
17. Display `0.25` as a percentage with one decimal place.
18. Right-align the word `"hi"` within a width of 8 characters.
19. Left-align the word `"hi"` within a width of 8 characters.
20. Centre the word `"hi"` within a width of 8 characters.
21. Pad the integer `7` to a width of 4 using leading zeros.
22. What does `f"{255:x}"` produce, and what does `:x` mean?
23. What does `f"{255:b}"` produce?
24. Predict the output:
    ```python
    print("A", end="-")
    print("B", end="-")
    print("C")
    ```
25. Predict the output of `print(1, 2, 3, sep="")`.
26. Why might output appear on separate lines when you expected one line?
27. Build a single f-string that prints `Total: $19.99` from a variable `total = 19.99`.
28. What is the difference between sending output to stdout and to stderr?
29. Write the line that prints `"error"` to standard error.
30. A program asks for a name and greets the user by it. Write the two lines that do this.
