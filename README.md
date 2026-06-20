# Python from Zero — A Beginner's Roadmap

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
![Level: Beginner](https://img.shields.io/badge/level-beginner-orange.svg)

A structured, no-fluff path for learning Python from your very first line of code to writing
your own classes. Every topic is a self-contained lesson: a concise explanation, reference
tables you can come back to, common pitfalls, and **30 of the most frequently asked questions**
with full worked solutions kept in a separate folder so you can test yourself honestly first.

This guide is written for the person who has never programmed before, but it does not talk down
to you. The goal is not just to make code *run* — it is to help you understand *why* it works,
which is exactly the difference between someone who copies snippets and someone a team wants to hire.

> **Python version:** All examples target **Python 3.10+** and are tested against the current
> stable release, **Python 3.14**. Grab the latest installer from
> [python.org/downloads](https://www.python.org/downloads/).

---

## Who this is for

- Complete beginners who want a clear order to learn things in.
- Self-taught learners filling gaps before interviews.
- Anyone who learns better by *doing the questions*, not just reading.

No prior programming experience is assumed. You only need a computer and about 30–45 focused
minutes per topic.

---

## How this repository is organised

```
python-beginner-guide/
├── README.md                 ← you are here (the roadmap)
├── LICENSE
├── .gitignore
├── topics/                   ← the lessons + practice questions
│   ├── 01-getting-started.md
│   ├── 02-variables-and-data-types.md
│   ├── 03-operators.md
│   └── ...
└── solutions/                ← worked answers (look here AFTER trying)
    ├── 01-getting-started-solutions.md
    ├── 02-variables-and-data-types-solutions.md
    ├── 03-operators-solutions.md
    └── ...
```

Each lesson file ends with **30 practice questions**. The matching file in `solutions/` holds the
answers and explanations. Keeping them apart is deliberate: the moment you can see the answer, you
stop thinking. Try first, struggle a little, *then* check.

---

## The roadmap

Work through these in order. Each builds on the one before it. The "Difficulty" column is relative
to a beginner, not to programming in general — everything here is foundational.

| #  | Topic                       | What you will be able to do                                             | Difficulty | Est. time |
|----|-----------------------------|-------------------------------------------------------------------------|------------|-----------|
| 01 | Getting Started             | Install Python, run code, use the shell, write & comment a first script | ★☆☆        | 30 min    |
| 02 | Variables & Data Types      | Store data, tell types apart, convert between them, understand mutability | ★☆☆      | 45 min    |
| 03 | Operators                   | Do maths, compare values, combine conditions, avoid precedence traps    | ★☆☆        | 40 min    |
| 04 | Strings                     | Slice, search, format, and transform text confidently                   | ★★☆        | 60 min    |
| 05 | Input & Output              | Read user input, format output, work with `print()` like a pro          | ★☆☆        | 30 min    |
| 06 | Conditional Statements      | Make decisions with `if` / `elif` / `else` and boolean logic            | ★★☆        | 45 min    |
| 07 | Loops                       | Repeat work with `for` and `while`; control flow with `break`/`continue`| ★★☆        | 60 min    |
| 08 | Lists                       | Build, index, slice, sort, and transform ordered collections           | ★★☆        | 60 min    |
| 09 | Tuples                      | Use immutable sequences, unpacking, and when to prefer them over lists  | ★★☆        | 30 min    |
| 10 | Dictionaries                | Map keys to values; the workhorse data structure of real Python code    | ★★☆        | 60 min    |
| 11 | Sets                        | Handle uniqueness and set maths (union, intersection, difference)       | ★★☆        | 30 min    |
| 12 | Functions                   | Write reusable code, pass arguments, return values, scope, `*args`/`**kwargs` | ★★★  | 75 min    |
| 13 | Modules & Packages          | Split code into files, use the standard library, install with `pip`     | ★★☆        | 45 min    |
| 14 | File Handling               | Read and write files safely with context managers                       | ★★☆        | 45 min    |
| 15 | Exceptions & Error Handling | Catch and raise errors with `try`/`except`/`finally`                     | ★★★        | 45 min    |
| 16 | Object-Oriented Programming | Define classes and objects, attributes, methods, and inheritance        | ★★★        | 90 min    |

> **Status:** Topics 01–03 are complete in this drop (lesson + 30 questions + full solutions each).
> The remaining topics follow the identical template and are being added in the same format.

---

## A suggested study path

If you have **a weekend**, do 01–07 — that's enough to write small, useful programs.

If you have **two weeks** at an hour a day, do the whole roadmap and rebuild each topic's questions
from memory the next day.

If you are **prepping for an interview**, skim the lessons but answer *every* question out loud as
if a person were asking you, then check the solution. The questions are written in the style
interviewers actually use.

### How to actually retain this

1. **Read** the lesson once, slowly.
2. **Type** every example yourself. Do not copy-paste — your fingers learn too.
3. **Break it on purpose.** Change a value, remove a line, and predict the error before you run it.
4. **Answer the 30 questions** before opening the solutions file.
5. **Come back in two days** and redo the ones you got wrong.

Reading code is not the same as knowing code. The questions are where the learning happens.

---

## The three lenses

Every lesson and every question in this repo is written from three points of view at once. If you
keep these in mind as you learn, you will pick up habits that take most self-taught programmers
years to develop:

- **The programmer** cares whether your code is *correct, readable, and idiomatic* — does it follow
  [PEP 8](https://peps.python.org/pep-0008/), does it use the right tool, will the next person
  understand it?
- **The teacher** cares whether you understand *why*, not just *what* — can you explain it to someone
  else without hand-waving?
- **The hiring manager** cares whether you know the *gotchas* — the `is` vs `==` traps, the mutable
  default argument, the `0.1 + 0.2` surprise — because those reveal real understanding.

Watch for the **"Watch out"** callouts in each lesson. Those are the things that separate "it works on
my machine" from "I know exactly what this does."

---

## Running the code

You can run any snippet in three ways:

| Method                | When to use it                            | How                                  |
|-----------------------|-------------------------------------------|--------------------------------------|
| Interactive shell     | Quick experiments, one-liners             | type `python` (or `python3`) in a terminal |
| Script file           | Anything more than a couple of lines      | save as `name.py`, then `python name.py` |
| Notebook / editor     | Learning step-by-step with notes          | VS Code, PyCharm, or Jupyter         |

A recommended free setup: **[VS Code](https://code.visualstudio.com/)** + the official Python
extension. It is what a large share of working developers use day to day.

---

## Contributing & feedback

Spotted a typo, a clearer explanation, or a better answer? Open an issue or a pull request. Learning
materials get better when more people poke holes in them. See [CONTRIBUTING.md](CONTRIBUTING.md) for
the short version of how.

## License

Released under the [MIT License](LICENSE) — free to use, copy, and adapt, including for your own
teaching. Attribution is appreciated but not required.
