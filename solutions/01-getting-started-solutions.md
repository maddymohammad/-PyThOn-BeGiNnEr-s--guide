# 01 · Getting Started — Solutions

Answers and explanations for the 30 questions in
[`topics/01-getting-started.md`](../topics/01-getting-started.md). Try the questions first.

---

**1. Define high-level, interpreted, dynamically typed.**
*High-level:* close to human language; hardware details are hidden. *Interpreted:* runs line by
line through an interpreter rather than being compiled to a standalone executable you manage.
*Dynamically typed:* you don't declare a variable's type; Python determines it at runtime.

**2. Creator and date.**
Guido van Rossum; first released in 1991.

**3. Version check command.**
`python --version` or, on systems where that fails, `python3 --version`. (`python -V` also works.)

**4. "Add Python to PATH."**
PATH is the list of folders your terminal searches for commands. Adding Python lets you type
`python` and `pip` from any directory. Skip it and the terminal replies "command not found," even
though Python is installed.

**5. REPL.**
Read–Eval–Print Loop. It **reads** your input, **evaluates** it, **prints** the result, then
**loops** back to wait for more.

**6. Exit the shell.**
Type `exit()` (or `quit()`), or press `Ctrl+Z` then Enter on Windows / `Ctrl+D` on macOS/Linux.

**7. Hello world.**
```python
print("Hello, world!")
```

**8. `print()` vs a comment.**
`print()` is executed and produces visible output. A comment is ignored by Python entirely; it
exists only for human readers.

**9. Three ways to run code.**
The **REPL** (quick experiments), a **script file** run with `python file.py` (real programs), and
an **editor/IDE** like VS Code (comfortable writing and debugging).

**10. Script extension.**
`.py`

**11. Run `app.py`.**
```bash
python app.py
```
(or `python3 app.py`)

**12. Comment about a discount.**
```python
discount = 0.10  # seasonal sale: 10% off until end of month
```

**13. Docstring.**
A string, usually triple-quoted, used as documentation — for example, the first statement inside a
function, class, or module. `"""Explain what this does."""`

**14. What vs why.**
A comment should explain *why*. The code already shows *what* it does; restating that is noise.
Comments earn their place by capturing intent, edge cases, or reasoning.

**15. Indentation size.**
Four spaces per level (PEP 8).

**16. Indentation errors.**
`IndentationError` and `TabError`.

**17. Tabs vs spaces.**
They look identical on screen but are different characters, so Python can't reliably tell how deeply
a line is indented. Python 3 forbids mixing them in the same block, raising `TabError`.

**18. Predicted output.**
```
A
B
```
`print("A")` is inside the `if True:` block; `print("B")` is not indented, so it runs regardless.

**19. Standard library vs pip package.**
The standard library ships *with* Python — no install needed (e.g. `math`, `random`, `os`). A pip
package is third-party code you download from PyPI with `pip install` (e.g. `requests`).

**20. Import math.**
```python
import math
```

**21. Installer and source.**
`pip` (or `pip3`); packages come from **PyPI**, the Python Package Index.

**22. macOS `python`.**
macOS historically shipped an outdated Python for system use that you shouldn't depend on; on modern
macOS, `python` may not exist at all. Install a current version and use `python3` / `pip3`.

**23. Smart quotes.**
Python raises a `SyntaxError`. It only recognises straight quotes (`"` `'`); the curly typographic
quotes a word processor inserts are different characters.

**24. Execution order.**
Top to bottom, one statement at a time, unless control flow (functions, loops, conditionals) changes
the path.

**25. Line continuation.**
End the line with a backslash `\`, or — cleaner — break the line inside parentheses, brackets, or
braces, where Python allows implicit continuation.

**26. `import this`.**
It prints the **Zen of Python**, a short set of aphorisms about Python's design philosophy.

**27. Two Zen principles.**
For example: *"Readability counts"* and *"There should be one — and preferably only one — obvious
way to do it."* The first means clear code matters more than clever code, because code is read far
more often than it is written.

**28. `Print("hi")`?**
No. Python is case-sensitive, and the built-in is the lowercase `print`. `Print` is undefined, so you
get a `NameError`.

**29. Writing vs running.**
Writing is composing/saving the text of your program in an editor. Running is handing that file to
the Python interpreter (via the terminal or a Run button) so it actually executes.

**30. Other uses of Python.**
Any two of: web back-ends (Django, Flask, FastAPI), automation/scripting, DevOps tooling, machine
learning and AI, scientific computing, testing, web scraping, game prototyping, finance.
