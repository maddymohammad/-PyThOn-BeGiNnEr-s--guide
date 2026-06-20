# 01 · Getting Started

> **You will be able to:** explain what Python is, install it, run code three different ways,
> write your first program, and comment it properly.

---

## What is Python?

Python is a **high-level**, **interpreted**, **general-purpose** programming language. Let's unpack
that, because each word matters:

| Term              | Plain-English meaning                                                                 |
|-------------------|---------------------------------------------------------------------------------------|
| High-level        | You write in something close to English; Python handles the messy hardware details.   |
| Interpreted       | Code runs line by line through an interpreter — no separate "compile" step you manage. |
| General-purpose   | Not built for one job. Used for web apps, data science, AI, automation, scripting, more. |
| Dynamically typed | You don't declare what type a variable is; Python figures it out at runtime.            |
| Multi-paradigm    | Supports several styles: procedural, object-oriented, and functional.                 |

It was created by **Guido van Rossum** and first appeared in **1991**. It is consistently one of the
most popular languages in the world, largely because it is *readable* — code you write today still
makes sense to you (and others) six months later.

### Why beginners are pointed at Python

- The syntax is clean and close to plain English, so you spend energy on *ideas*, not punctuation.
- A massive ecosystem of free libraries means you rarely start from scratch.
- It is used professionally in nearly every field, so the skill transfers to real jobs.

---

## Installing Python

Download the latest release from **[python.org/downloads](https://www.python.org/downloads/)**.
Anything **3.10 or newer** is fine for this guide; the current stable version is **3.14**.

| OS       | Notes                                                                                          |
|----------|------------------------------------------------------------------------------------------------|
| Windows  | Run the installer and **tick "Add Python to PATH"** before clicking Install. This one checkbox saves hours of confusion. |
| macOS    | Download the installer, or use [Homebrew](https://brew.sh/): `brew install python`. macOS ships with an old Python you should not rely on. |
| Linux    | Usually preinstalled. Install the latest with your package manager, e.g. `sudo apt install python3`. |

### Check it worked

Open a terminal (Command Prompt / PowerShell on Windows, Terminal on macOS/Linux) and run:

```bash
python --version
```

If that says "command not found," try `python3 --version`. You should see something like
`Python 3.14.0`.

> **Watch out:** On macOS and many Linux systems, `python` may not exist at all, or may point to an
> ancient version. Use `python3` and `pip3` there. On Windows after a normal install, `python` is correct.

---

## Three ways to run Python

| Way                  | Best for                                  | How to start it                          |
|----------------------|-------------------------------------------|------------------------------------------|
| Interactive shell (REPL) | Trying one idea, doing quick maths     | Type `python` and press Enter            |
| Script file          | Real programs of more than a line or two  | Save a `.py` file, then `python file.py` |
| Editor / IDE         | Writing and debugging comfortably         | VS Code, PyCharm, IDLE, or Jupyter       |

**REPL** stands for *Read–Eval–Print Loop*: it reads what you type, evaluates it, prints the result,
and waits for the next line. Type `exit()` to leave it.

```python
>>> 2 + 2
4
>>> "hello".upper()
'HELLO'
```

---

## Your first program

Create a file called `hello.py` with one line:

```python
print("Hello, world!")
```

Run it:

```bash
python hello.py
```

Output:

```
Hello, world!
```

`print()` is a **built-in function**. The text inside the quotes is a **string** — a piece of text.
The parentheses are how you *call* a function and pass it something to work with.

> **Watch out:** Quotes must match and be straight quotes (`"` or `'`), not the curly "smart quotes"
> a word processor inserts. Copying code out of a Word document is a classic beginner trap.

---

## Comments

Comments are notes for humans; Python ignores them when running.

```python
# This is a single-line comment
print("Hi")  # comments can also sit at the end of a line

"""
A triple-quoted string used as a block of notes.
Technically a string, commonly used for multi-line documentation (a "docstring").
"""
```

| Style              | Syntax        | Use it for                            |
|--------------------|---------------|---------------------------------------|
| Single-line        | `# ...`       | Quick notes, explaining a tricky line |
| End-of-line        | `code  # ...` | Clarifying a specific statement       |
| Docstring          | `""" ... """` | Documenting modules, functions, classes |

Good comments explain **why**, not **what**. `x = x + 1  # add one to x` is noise; the code already
says that.

---

## Indentation: Python's most important rule

Most languages use braces `{ }` to group code. **Python uses indentation** (whitespace) instead.
Lines that belong together must be indented the same amount.

```python
if True:
    print("indented, so this belongs to the if")
    print("so does this")
print("not indented, runs no matter what")
```

The standard is **4 spaces** per level. Mixing tabs and spaces causes errors that are maddening to
spot, so configure your editor to insert spaces when you press Tab.

> **Watch out:** `IndentationError` and `TabError` are among the first errors every beginner meets.
> They almost always mean a line is indented inconsistently with its neighbours.

---

## How code is read

A `.py` file runs **top to bottom**, one statement per line by default. A statement is a complete
instruction.

```python
name = "Ada"          # statement 1
greeting = "Hello"    # statement 2
print(greeting, name) # statement 3 -> Hello Ada
```

You can split a long line with a backslash `\`, but it is usually cleaner to break inside
parentheses, brackets, or braces, where Python allows line breaks automatically.

---

## `pip` and the standard library

Python comes with a huge **standard library** — modules bundled in, ready to use:

```python
import math
print(math.sqrt(16))  # 4.0
```

For anything *not* bundled, you install packages from PyPI (the Python Package Index) with **pip**:

```bash
pip install requests        # or pip3 on macOS/Linux
```

You will learn modules and packages properly in lesson 13 — for now just know the two ideas exist.

---

## The Zen of Python

Run this once in the shell; it prints the guiding philosophy of the language:

```python
import this
```

Two lines worth remembering early: *"Readability counts"* and *"There should be one — and preferably
only one — obvious way to do it."*

---

## Quick recap

- Python is high-level, interpreted, dynamically typed, and used almost everywhere.
- Install from python.org; verify with `python --version` (or `python3`).
- Run code in the **REPL**, as a **script**, or in an **editor**.
- `print()` shows output; strings go in matching straight quotes.
- Comments (`#` and docstrings) are for humans.
- **Indentation is syntax**, not decoration — 4 spaces per level.

---

## Practice questions

Try every one before opening
[`solutions/01-getting-started-solutions.md`](../solutions/01-getting-started-solutions.md).

1. In one sentence each, define "high-level," "interpreted," and "dynamically typed."
2. Who created Python and roughly when did it first appear?
3. What command checks your installed Python version? Give the two common variants.
4. Why does the Windows installer ask you to "Add Python to PATH," and what breaks if you skip it?
5. What does REPL stand for, and what does each part do?
6. How do you exit the interactive shell?
7. Write the single line of code that prints `Hello, world!`.
8. What is the difference between `print()` and a comment?
9. Name the three ways to run Python code and when you'd choose each.
10. What file extension do Python scripts use?
11. What is the command to run a script file named `app.py`?
12. Write a single-line comment that explains why a discount is 10%.
13. What is a docstring, and how is it written?
14. Should a comment explain *what* the code does or *why*? Give a reason.
15. How many spaces is one level of indentation, by convention?
16. What two error names typically appear when indentation is wrong?
17. Why is mixing tabs and spaces a problem in Python?
18. Predict the output:
    ```python
    if True:
        print("A")
    print("B")
    ```
19. What is the difference between the standard library and a package installed with pip?
20. Write the line that imports the `math` module.
21. What tool installs third-party packages, and where do they come from?
22. On macOS, why might `python` point to the wrong version, and what should you use instead?
23. What happens if you use curly "smart quotes" from a word processor in your code?
24. By default, in what order are the statements in a `.py` file executed?
25. How can you continue one logical line of code across two physical lines?
26. What does `import this` print, and what is it called?
27. Quote two principles from the Zen of Python and explain one in your own words.
28. Is `Print("hi")` (capital P) valid Python? Why or why not?
29. What is the difference between *writing* code in an editor and *running* it in a terminal?
30. A friend says "Python is only for data science." Give two other real-world uses to correct them.
