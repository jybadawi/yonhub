# 📘 Learn YonderScript

A friendly, complete guide to **YonderScript** — a small, readable programming language. If you've never coded before, start at the top and work down. Each section has examples you can run.

> **How to run examples:** put code in a file like `hello.ys` and run `yon hello.ys`, or type `yon` for the interactive prompt.

---

## Contents
1. [Hello, world](#1-hello-world)
2. [Comments](#2-comments)
3. [Variables & values](#3-variables--values)
4. [Printing with `say`](#4-printing-with-say)
5. [Math & operators](#5-math--operators)
6. [Text (strings)](#6-text-strings)
7. [Truth & logic](#7-truth--logic)
8. [Making decisions: `when`](#8-making-decisions-when)
9. [Loops: `whilst` and `foreach`](#9-loops-whilst-and-foreach)
10. [Lists](#10-lists)
11. [Maps](#11-maps)
12. [Functions: `task`](#12-functions-task)
13. [Lambdas (quick functions)](#13-lambdas)
14. [Classes: `blueprint`](#14-classes-blueprint)
15. [Handling errors](#15-handling-errors)
16. [Libraries: `bring` & `yon install`](#16-libraries)
17. [The `yon` tools](#17-the-yon-tools)
18. [Cheat sheet](#18-cheat-sheet)

---

## 1. Hello, world

```
say "Hello, world!"
```

`say` prints things to the screen. That's your first program.

## 2. Comments

Anything after a `~` is a note for humans; YonderScript ignores it.

```
~ this is a comment
say "hi"   ~ you can put one at the end of a line too
```

## 3. Variables & values

Store a value with `=`. No special keyword needed.

```
name = "Jonathan"
age = 21
say name, age
```

The basic value types:

| Type | Example |
| --- | --- |
| number | `42`, `3.14` |
| text | `"hello"` |
| truth | `yes`, `no` |
| nothing | `nothing` |
| list | `[1, 2, 3]` |
| map | `{"a": 1}` |

Check a value's type with `kind`:

```
say kind(42)        ~ number
say kind("hi")      ~ text
say kind(yes)       ~ truth
```

## 4. Printing with `say`

`say` takes one or more things, separated by commas:

```
say "the answer is", 42
```

**f-strings** drop values right into text with `{ }`:

```
name = "Sam"
say f"Hi {name}, you have {3 + 4} messages"
```

## 5. Math & operators

```
say 2 + 3        ~ 5
say 10 - 4       ~ 6
say 6 * 7        ~ 42
say 20 / 4       ~ 5
say 17 % 5       ~ 2   (remainder)
say 2 ** 8       ~ 256 (power)
```

Shortcuts update a variable in place:

```
score = 10
score += 5       ~ now 15
score *= 2       ~ now 30
```

## 6. Text (strings)

Join text with `+`, and use handy methods:

```
first = "yonder"
say first + "script"          ~ yonderscript
say first.upper()             ~ YONDER
say "  hi  ".trim()           ~ hi
say "a,b,c".split(",")        ~ [a, b, c]
say "hello".has("ell")        ~ yes
say "hello"[0]                ~ h        (indexing)
say "hello"[1:4]              ~ ell      (slicing)
```

## 7. Truth & logic

`yes` and `no` are the truth values. Combine conditions with `also` (and), `alt` (or), `notso` (not):

```
age = 20
say age >= 18 also age < 65   ~ yes
say age < 13 alt age > 65     ~ no
say notso yes                 ~ no
```

Comparisons: `==` `!=` `<` `<=` `>` `>=`.

## 8. Making decisions: `when`

```
age = 20
when age >= 18:
    say "adult"
elsewhen age >= 13:
    say "teen"
otherwise:
    say "kid"
end
```

There's also an **inline** version for picking a value:

```
label = "adult" when age >= 18 otherwise "minor"
say label
```

## 9. Loops: `whilst` and `foreach`

`whilst` repeats while a condition is true:

```
count = 1
whilst count <= 3:
    say "count", count
    count += 1
end
```

`foreach` walks through a list (or text, or map):

```
foreach fruit in ["apple", "pear", "plum"]:
    say fruit
end

foreach n in upto(1, 6):     ~ upto(1,6) = 1,2,3,4,5
    say n
end
```

Use `stop` to break out of a loop, `skip` to jump to the next round.

## 10. Lists

```
nums = [10, 20, 30]
say nums[0]              ~ 10
say len(nums)            ~ 3
push(nums, 40)           ~ add to the end
say nums                 ~ [10, 20, 30, 40]
say sum(nums)            ~ 100
say nums[1:3]            ~ [20, 30]   (slice)
```

**Comprehensions** build a list in one line:

```
squares = [n * n foreach n in upto(1, 6)]      ~ [1, 4, 9, 16, 25]
evens = [n foreach n in upto(10) when n % 2 == 0]
```

## 11. Maps

Maps store values by a key:

```
person = {"name": "Sam", "age": 30}
say person["name"]       ~ Sam
person["age"] = 31       ~ change it
say person.keys()        ~ [name, age]
say person.has("name")   ~ yes
```

## 12. Functions: `task`

```
task greet(who):
    giveback "Hello, " + who
end

say greet("world")
```

Functions can have **default** and **keyword** arguments:

```
task greet(who, greeting = "Hello"):
    giveback greeting + ", " + who
end

say greet("world")                    ~ Hello, world
say greet("world", greeting = "Yo")   ~ Yo, world
```

## 13. Lambdas

A lambda is a quick, unnamed function: `fn(args) => result`.

```
double = fn(x) => x * 2
say double(21)           ~ 42
```

They're great with list tools (install the `lists` library):

```
bring "lists"
say lists.map([1, 2, 3, 4], fn(x) => x * x)   ~ [1, 4, 9, 16]
```

## 14. Classes: `blueprint`

A `blueprint` describes a kind of thing. `setup` runs when you create one, and `me` refers to the thing itself.

```
blueprint Dog:
    task setup(name):
        me.name = name
    end
    task speak():
        giveback me.name + " says woof"
    end
end

rex = Dog("Rex")
say rex.speak()          ~ Rex says woof
```

Blueprints can build on others with `from`, and call the parent version with `base`:

```
blueprint Puppy from Dog:
    task speak():
        giveback base.speak() + " (yip!)"
    end
end

say Puppy("Bo").speak()   ~ Bo says woof (yip!)
```

## 15. Handling errors

Wrap risky code in `attempt`; catch problems with `rescue`; `ensure` always runs.

```
attempt:
    n = num("not a number")
rescue err:
    say "that failed:", err
ensure:
    say "done trying"
end
```

Raise your own error with `raise`:

```
raise "something went wrong"
```

## 16. Libraries

Bring in a library with `bring`, then use its tasks:

```
bring "jokes"
say jokes.tell()
```

Install libraries with `yon install` (they come from the online registry):

```bash
yon install jokes
yon install mathx
yon search          # see what's available
```

You also get **all of Python's libraries** for free — just `bring` them:

```
bring "math"
say math.sqrt(144)      ~ 12
bring "random"
say random.randint(1, 6)
```

Install a Python library too:

```bash
yon install --py numpy
```

## 17. The `yon` tools

| Command | What it does |
| --- | --- |
| `yon` | interactive prompt (numbered lines + `run`, shell commands, and live code) |
| `yon file.ys` | run a program |
| `yon shell` | a terminal that speaks YonderScript |
| `yon serve p8000` | serve the current folder over HTTP |
| `yon install <name>` | install a library |
| `yon search` | list available libraries |
| `yon make <name>` | start a new library |

## 18. Cheat sheet

| Idea | Python | YonderScript |
| --- | --- | --- |
| print | `print` | `say` |
| if / elif / else | `if`/`elif`/`else` | `when`/`elsewhen`/`otherwise` … `end` |
| while | `while` | `whilst` … `end` |
| for | `for x in` | `foreach x in` … `end` |
| function | `def` | `task` … `end` |
| return | `return` | `giveback` |
| True / False | `True`/`False` | `yes` / `no` |
| None | `None` | `nothing` |
| and / or / not | `and`/`or`/`not` | `also` / `alt` / `notso` |
| break / continue | `break`/`continue` | `stop` / `skip` |
| class | `class` | `blueprint` |
| import | `import` | `bring` |
| try / except / finally | `try`/`except`/`finally` | `attempt`/`rescue`/`ensure` |
| comment | `#` | `~` |

---

### A complete little program

```
bring "jokes"

task countdown(n):
    whilst n > 0:
        say n
        n -= 1
    end
    say "Here's a joke:"
    say jokes.tell()
end

countdown(3)
```

That's YonderScript! Explore the [libraries](README.md), and have fun out in the yonder. ✨
