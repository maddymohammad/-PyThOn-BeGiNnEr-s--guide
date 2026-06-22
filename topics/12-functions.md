# 12 · Functions

> **You will be able to:** define and call functions, pass arguments in every form, return values,
> understand scope, and avoid the mutable-default-argument trap that catches even experienced people.

---

## Why functions?

A function is a named, reusable block of code. Instead of repeating logic, you write it once and
*call* it whenever you need it. Functions make code shorter, easier to test, and easier to read —
each one does a named job.

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Ada")      # Hello, Ada!
greet("Linus")    # Hello, Linus!
```

`def` starts the definition, `greet` is the name, `name` is a **parameter**, and the indented lines
are the body. When you write `greet("Ada")`, the value `"Ada"` is an **argument**.

> **Terminology:** a *parameter* is the variable in the definition; an *argument* is the actual value
> you pass when calling. People use them loosely, but interviewers like the distinction.

---

## Returning values

`return` sends a value back to the caller. A function **without** a `return` (or with a bare `return`)
gives back `None`.

```python
def add(a, b):
    return a + b

result = add(2, 3)    # 5

def shout(text):
    print(text.upper())   # prints, but returns nothing

x = shout("hi")       # prints HI, and x is None
```

> **Watch out — print vs return:** printing shows text on screen; returning hands a value back so
> your code can *use* it. `x = print("hi")` makes `x` equal to `None`. If you need the value later,
> `return` it; don't just print it.

`return` also exits the function immediately:

```python
def first_even(numbers):
    for n in numbers:
        if n % 2 == 0:
            return n        # leaves the function as soon as one is found
    return None
```

Return several values by separating them with commas — they come back as a tuple (lesson 9):

```python
def min_max(nums):
    return min(nums), max(nums)

low, high = min_max([3, 1, 7])   # low=1, high=7
```

---

## Default parameter values

Give a parameter a default and it becomes optional:

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

greet("Ada")             # 'Hello, Ada!'
greet("Ada", "Hi")       # 'Hi, Ada!'
```

> **Watch out:** parameters *with* defaults must come **after** parameters without them. `def f(a=1, b)`
> is a `SyntaxError`.

---

## Positional vs keyword arguments

```python
def describe(name, age, city):
    return f"{name}, {age}, from {city}"

describe("Ada", 36, "London")                       # positional — order matters
describe(name="Ada", city="London", age=36)         # keyword — order doesn't
describe("Ada", city="London", age=36)              # mix: positional first, then keyword
```

| Style       | How it's matched         | Order matters? |
|-------------|--------------------------|----------------|
| Positional  | by position              | yes            |
| Keyword     | by parameter name        | no             |

> **Watch out:** once you use a keyword argument in a call, every argument after it must also be a
> keyword. `describe(name="Ada", 36, "London")` is a `SyntaxError`.

---

## `*args` and `**kwargs` — variable arguments

`*args` collects extra **positional** arguments into a **tuple**; `**kwargs` collects extra **keyword**
arguments into a **dict**:

```python
def total(*args):
    return sum(args)         # args is a tuple

total(1, 2, 3, 4)            # 10

def show(**kwargs):
    return kwargs            # kwargs is a dict

show(a=1, b=2)               # {'a': 1, 'b': 2}
```

The names `args` and `kwargs` are convention; it's the `*` and `**` that matter. The full parameter
order in a definition is: positional, then `*args`, then keyword-only, then `**kwargs`.

You can also *unpack* into a call with `*` and `**`:

```python
nums = [1, 2, 3]
print(total(*nums))          # same as total(1, 2, 3)
```

---

## Scope: local vs global

Variables created **inside** a function are *local* — they exist only during the call and can't be
seen outside:

```python
def f():
    x = 10        # local to f
    print(x)

f()               # 10
print(x)          # NameError: x is not defined
```

You can **read** a global variable from inside a function, but **assigning** to a name makes it local.
To modify a global, declare it with `global` (use this sparingly — it's often a sign to restructure):

```python
count = 0
def increment():
    global count
    count += 1

increment()
print(count)      # 1
```

Python resolves names by the **LEGB** rule — Local, Enclosing, Global, Built-in — searching those
scopes in that order.

> **Watch out:** without `global`, `count += 1` inside the function would raise an
> `UnboundLocalError`, because the assignment makes `count` local, yet you're reading it before it's
> assigned.

---

## The mutable default argument trap

This is the single most famous Python gotcha. A default value is created **once**, when the function
is defined — not on each call. So a mutable default like `[]` is *shared* across every call:

```python
def add_item(item, items=[]):     # BUG
    items.append(item)
    return items

print(add_item(1))     # [1]
print(add_item(2))     # [1, 2]   <- the SAME list persisted!
print(add_item(3))     # [1, 2, 3]
```

The fix is to default to `None` and create a fresh list inside:

```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(1))     # [1]
print(add_item(2))     # [2]   <- fresh each time
```

> **Watch out:** never use a mutable object (`[]`, `{}`, `set()`) as a default parameter value.
> Default to `None` and build the real value in the body.

---

## Docstrings

A string as the first line of a function documents it and shows up in `help()`:

```python
def area(radius):
    """Return the area of a circle with the given radius."""
    return 3.14159 * radius ** 2
```

---

## Lambdas (anonymous functions)

A `lambda` is a tiny one-expression function, handy where a function is needed briefly (e.g. a sort
key):

```python
square = lambda x: x * x
print(square(5))                 # 25

words = ["pear", "fig", "banana"]
words.sort(key=lambda w: len(w)) # sort by length
```

> **Watch out:** for anything beyond a single simple expression, use a normal `def` — it's clearer
> and can have a docstring. Don't assign a lambda to a name just to act like a function; use `def`.

---

## Type hints (a quick note)

Hints document the expected types. They don't enforce anything at runtime, but they help readers and
tools:

```python
def add(a: int, b: int) -> int:
    return a + b
```

---

## Quick recap

- `def name(params):` defines a function; arguments are the values you pass when calling.
- `return` sends a value back and exits the function; no `return` means it returns `None`.
- *Printing* shows text; *returning* gives a value your code can use — they're not the same.
- Defaults make parameters optional and must come after non-default parameters.
- Arguments can be **positional** (by order) or **keyword** (by name); keywords come after positionals.
- `*args` gathers extra positionals into a **tuple**; `**kwargs` gathers extra keywords into a **dict**.
- Names assigned in a function are **local**; use `global` (sparingly) to modify a global. Lookup is **LEGB**.
- **Never** use a mutable default (`[]`/`{}`) — default to `None` and create it inside.
- Document with a docstring; use `lambda` only for tiny one-off expressions.

---

## Practice questions

Try every one before opening
[`solutions/12-functions-solutions.md`](../solutions/12-functions-solutions.md).

1. What keyword defines a function, and what makes up its body?
2. What's the difference between a parameter and an argument?
3. Write a function `add(a, b)` that returns their sum, then call it with `2` and `3`.
4. What does a function return if it has no `return` statement?
5. Predict and explain: `x = print("hi")`. What is `x`?
6. In your own words, what's the difference between printing a value and returning it?
7. Besides giving back a value, what else does `return` do to the function's execution?
8. Write a function that returns the first even number in a list, or `None` if there isn't one.
9. How does a function return more than one value, and how do you receive them?
10. Add a default so `greet(name, greeting="Hello")` can be called with just a name.
11. Why must `def f(a=1, b)` fail? State the rule.
12. Call `describe(name, age, city)` using all keyword arguments in a different order.
13. Can you put a positional argument *after* a keyword argument in a call? What happens?
14. What does `*args` collect, and what type is it inside the function?
15. What does `**kwargs` collect, and what type is it inside the function?
16. Write a function `total(*args)` that returns the sum of all arguments passed.
17. Given `nums = [1, 2, 3]`, call `total` so it receives them as three separate arguments.
18. What's the correct order of parameter kinds in a function definition?
19. Predict the output:
    ```python
    def f():
        x = 10
    f()
    print(x)
    ```
20. Can a function read a global variable without any special keyword? Can it reassign one?
21. What keyword lets a function modify a global variable, and why should it be used sparingly?
22. What does LEGB stand for?
23. Why does `count += 1` inside a function (with `count` a global) raise `UnboundLocalError` without `global`?
24. Predict the output and explain the bug:
    ```python
    def add_item(item, items=[]):
        items.append(item)
        return items
    print(add_item(1))
    print(add_item(2))
    ```
25. Why does the mutable-default bug happen? When is the default created?
26. Rewrite `add_item` correctly so each call starts with a fresh list.
27. What is a docstring, where does it go, and what reads it?
28. Write a `lambda` that squares its argument, and call it with `5`.
29. When should you use a `lambda`, and when should you prefer a normal `def`?
30. What do type hints like `def add(a: int, b: int) -> int:` do at runtime?
