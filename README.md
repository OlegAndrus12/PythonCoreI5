# Python Core

**English** · [Українська](README.uk.md)

[![Python](https://img.shields.io/badge/Python-3.14-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/downloads/)

Lecture materials for the Python Core course. Each module is one lecture: slides, a lecture plan, and
interactive pages and scripts that make **one idea** concrete — run it, change it, read why the output
changed.

Modules are added as lectures happen; the complete previous iteration is [PythonCoreI4](https://github.com/OlegAndrus12/PythonCoreI4).

<img src="yoda.jpg" alt="May the Force be with you" width="280"> <img src="module01/duck_test.jpg" alt="A dog, a fish, a bird and a duck: each wishes it could do what the others do; the duck can walk, swim and fly" width="280">

## Getting the materials

Download the course once:

```bash
git clone https://github.com/OlegAndrus12/PythonCoreI5.git
cd PythonCoreI5
```

Before each lecture, get the new materials from inside that folder:

```bash
git pull
```

No login is needed: the repository is public. New to Git, or something went wrong?
👉 **[Step-by-step guide: install Git, clone, pull, HTTPS and SSH authentication, fixing common errors](GIT_GUIDE.md)**

> Keep your own exercises **outside** the course folder, so that `git pull` never conflicts with your changes.

## Modules

```
├── module01/   Data types: built-in types, mutability, typing, operator precedence, collections, keywords, conversions
```

**Conventions used throughout:**

- Each module has an `agenda.md` with the lecture plan (in Ukrainian); slides are added as a PDF where there are any.
- The `.html` pages are self-contained: open them straight from disk in a browser (double-click the file), no server or install needed.
- Every result shown in an HTML page comes from actually running that example on CPython 3.14.3.
- Every script runs on its own: `python module01/strings/basics.py`. `module01/deposit.py` asks for input.

---

# Module 01 — Data types

What every built-in type is, what it can do, and the ideas that explain most beginner surprises:
names are references, some objects change in place and others never do, and Python checks types at
runtime but never converts them silently.

| File                                                    | What it is                                                                                                                                                                                         |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[lecture notes.html](module01/lecture%20notes.html)** | Interactive cheat sheet (in Ukrainian): one tab per built-in type, five topic tabs and a glossary (below)                                                                                         |
| **[visualizer.html](module01/visualizer.html)**         | Type `a = [1, "hi", True]`, `b = a`, `a.append(99)`, `del a` and watch names point at objects on the heap — with reference counts, small-int interning, garbage collection and the bytecode for each line |
| **[Intro.pdf](module01/Intro.pdf)**                     | Lecture slides                                                                                                                                                                                     |
| [duck_test.jpg](module01/duck_test.jpg)                 | Duck typing, illustrated                                                                                                                                                                           |

**Example scripts** — each one a real-world scenario (a song, a playlist, a deposit):

| Script                                                  | What it shows                                                                                                                                  |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [strings/basics.py](module01/strings/basics.py)         | Three ways to format a string, multiline strings, case methods, search and check, modify, split and join, slicing, `IndexError`                |
| [tuples/basics.py](module01/tuples/basics.py)           | Creating (and the single-element trailing comma), accessing, unpacking, immutability, methods, tuple vs list, tuples as dict keys             |
| [tuples/use_cases.py](module01/tuples/use_cases.py)     | Eight real uses: coordinates, returning several values, unpacking CSV rows, composite keys, deduplicating records, swap, constants, sort keys  |
| [conversions/basics.py](module01/conversions/basics.py) | Converting between `int`, `float`, `bool`, `None`, `str`, `list`, `set` and `dict`, which conversions fail and why, and chained conversions    |
| [deposit.py](module01/deposit.py)                       | A compound-interest calculator: reads three numbers with `input()`, converts them with `float()`, uses `math.pow` and `math.floor`              |

**The cheat sheet, tab by tab:**

| Tab                                                   | What's in it                                                                                                                                                         |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `int` `str` `bool` `None` `list` `dict` `tuple` `set` | Literals, key properties, the operations that trip people up, and every public method with an example (rarely used ones folded away). `bool` adds a truth table      |
| **Змінність** — mutability                            | A map of mutable vs immutable types; memory diagrams of `b.append()` vs `t += '!'`; consequences for dict keys, default arguments and copying                        |
| **Типізація** — typing                                | Static/dynamic × strong/weak on one chart; when a type error is caught (compile time, runtime, or mypy); the same expression in Python, JavaScript and Java          |
| **Пріоритети** — operator precedence                  | The short version to remember, then all 18 levels with associativity, an expression tree for `1 + 2 * 3 ** 2 > 10 and not False`, and traps like `-2 ** 2`            |
| **Колекції** — collections                            | `list` / `tuple` / `set` / `dict` / `str` side by side, the Big-O of each operation, why `in` is O(1) for a set, and a "which one do I need?" flowchart              |
| **Порівняння** — comparison                           | All eight types in one table                                                                                                                                         |
| **Словник** — glossary                                | All 35 Python keywords and 4 soft keywords grouped by purpose, each group with runnable examples, plus plain-language definitions of the terms used on the page      |

📋 Full topic list: **[module01/agenda.md](module01/agenda.md)**
