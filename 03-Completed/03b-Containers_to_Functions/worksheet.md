# 📝 Worksheet: 03b - Containers → Functions

Do this worksheet **on paper, without a computer**. The point is to practice being the computer. Each section ends with an **🤖 Explain It** prompt: write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Trace a Loop

Fill in the table for this code:

```python
temps = [31, 45, 28, 52]
total = 0
count = 0
for t in temps:
    total += t
    if t <= 32:
        count += 1
```

| pass | `t` | `total` | `count` |
|------|-----|---------|---------|
| start | — | 0 | 0 |
| 1 | 31 | 31 | 1 |
| 2 | 45 | 76 | 1 |
| 3 | 28 | 104 | 2 |
| 4 | 52 | 156 | 2 |

Which **two** patterns are mixed together in this loop?  
`Answer:` **Accumulate + Count**

> 🤖 **Explain It:** Explain the difference between Accumulate, Count, and Filter as if you were talking to someone who has never programmed.

**Accumulate: You keep a running total. Like adding up all your receipts to see how much you spent.**
**Count: You tally how many things match a condition. Like counting how many students scored above 90.**
**Filter: You keep only the items that match a condition. Like making a new list of only the passing scores.**

---

## 🧠 Section 2: Pick Your Weapon

| Scenario | Container | Why? |
|----------|-----------|------|
| Daily step counts for a month | list | Ordered, fixed-length sequence. |
| A playing card (rank, suit) | tuple | Two fixed parts that never change meaning. |
| Username → password hash | dict | Key -> value lookup. |
| Every distinct IP address in a log file | set | Automatically removes duplicates. |
| Your class schedule, in order | list | Order matters. |

> 🤖 **Explain It:** Pick the scenario you were *least* sure about and argue for a different container than the one you chose.

**I was least sure about `Your class schedule, in order`. A dictionary could be used instead because then you could look up a class by name.**

---

## 🧠 Section 3: Take It Apart

```python
course = {
    "title": "CMPS 3603",
    "students": [
        {"name": "Ana", "scores": [88, 92]},
        {"name": "Ben", "scores": [75, 81]}
    ]
}
```

Write the value after **each** step:

1. `course["students"]` → **[{"name": "Ana", "scores": [88, 92]}, {"name": "Ben", "scores": [75, 81]}]**
2. `course["students"][1]` → **{"name": "Ben", "scores": [75, 81]}**
3. `course["students"][1]["scores"]` → **[75, 81]**
4. `course["students"][1]["scores"][0]` → **75**

Write the expression that gets Ana's second score:  
`Answer:` **course["students"][0]["scores"][1]**

---

## 🧠 Section 4: Functions

1. What prints?

```python
def f(x):
    return x + 1

print(f(f(f(0))))
```

   `Answer:` **3**

2. What prints? Explain why.

```python
def shout(word):
    print(word.upper())

x = shout("hi")
print(x)
```

   `Answer:` **`HI` then `None` because shout does not return anything, so Python gives it the default return value: `None`.**

3. Circle the **parameters** and underline the **arguments**:

```python
def greet(name, greeting):
    return greeting + ", " + name

greet("Ada", "Hello")
```

**Circled parameters: `name` and `greeting`**
**Underlined arguments: `"Ada"` and `"Hello"`**

> 🤖 **Explain It:** In your own words, explain `print()` vs. `return`. Then explain why getting it wrong breaks a pipeline.

**`print()` displays output to the screen while `return` gives a value back to the caller so another function can use it. Getting it wrong breaks a pipline because printed output cannot be used as data.**

---

## 🧠 Section 5: Contracts and Tests

Write a contract for a function `longest_word(words)`:

```text
IN: a list of strings
OUT: the single longest string
DOES: scans through the list and returns the longest word 
```

Write one test of each kind:

- Normal: **longest_word(["cat", "giraffe", "dog"]) -> "giraffe"**
- Boundary: **longest_word(["hi"]) -> "hi"**
- Weird: **longest_word([]) -> None**

---

## 🧠 Section 6: Draw the Pipeline

> "Given a list of prices, drop any that are `0` or less, add 8.25% tax to each, then find the total."

1. Name each function you'd need.
- **drop_free(prices)**
- **add_tax(prices)**
- **total(prices)**

2. For each one, write what goes **in** and what comes **out** (shape, not just "data").
- **drop_free: list -> list**
- **add_tax: list -> list**
- **total: list -> number**

3. Draw the pipeline with arrows, labeling each arrow with the data's shape.
[prices] 
    ↓ (list → list)
drop_free
    ↓ (list → list)
add_tax
    ↓ (list → number)
total

> 🤖 **Explain It:** Why is a pipeline of small functions easier to fix than one big block of code?

**Small functions isolate mistakes. If your tax is wrong, you fix one function. If your filtering is wrong, you fix one function. In a giant block of coode, everything is tangled. Changing one part risks breaking another. Pipelines keep logic modular, testable, and predictable.**