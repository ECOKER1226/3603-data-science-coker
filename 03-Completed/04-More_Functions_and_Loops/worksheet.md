# 📝 Worksheet: 04 - More Functions & Loops

Do this worksheet **on paper, without a computer**. Each section ends with an **🤖 Explain It** prompt: write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Defaults and Keywords

```python
def price(amount, tax=0.0825, discount=0):
    return round(amount * (1 + tax) - discount, 2)
```

What does each call return?

1. `price(100)` → **`108.25`**
2. `price(100, discount=10)` → **`98.25`**
3. `price(100, 0)` → **`100.00`**
4. `price(discount=5, amount=20)` → **`16.65`**

> 🤖 **Explain It:** Why are keyword arguments easier to read than positional ones in a call like `price(100, 0, 10)`?

**Because keyword arguments rely on name so you don't have to remember or look up the position of each argument.**

---

## 🧠 Section 2: Scope

What prints? Explain why.

```python
count = 0

def add_one(count):
    count = count + 1
    return count

result = add_one(count)
print(count, result)
```

`Answer:` **`0 1` because `print(count, result)` calls `count` outside of the function before calling the `result` of `add_one(count)`.**

> 🤖 **Explain It:** Describe the "room with two doors" model of a function in your own words.

**`Arguments` enter through the `parameters` door of the function and leave through the `return` door.**

---

## 🧠 Section 3: Trace a While Loop

```python
balance = 100
years = 0
while balance < 150:
    balance = balance + 20
    years += 1
```

| pass | `balance` at the start | `balance < 150`? | `balance` after | `years` after |
|------|------------------------|------------------|-----------------|---------------|
| 1 | 100 | yes | 120 | 1 |
| 2 | 120 | yes | 140 | 2 |
| 3 | 140 | yes | 160 | 3 |
| 4 | 160 | no | 160 | 3 |

Final `years`: **3**  Final `balance`: **160**

What single change would make this an **infinite** loop?  
`Answer:` **By changing `balance = balance + 20` to `balance = balance - 20`.**

---

## 🧠 Section 4: `for` or `while`?

| Task | `for` or `while`? | Why? |
|------|-------------------|------|
| Print each line of a file | for | You know how many lines are in a file. |
| Keep asking for a password until it's correct | while | You don't know how many times an incorrect password may be given. |
| Find the average of a list of prices | for | You know how many items are in a list. |
| Double a number until it's over one million | while | You don't know how many times a number may need to be doubled. |

---

## 🧠 Section 5: Files

Given the file `pets.txt`:

```text
name,species
Rex,dog

# rescued in May
Tom,cat
```

1. How many times does `for line in f:` run? **5**
2. Which lines should your code skip, and how would you detect each one?  
   `Answer:` **Skip `name,species` and detect it with `if line.startswith("name"):`, skip the `blank` line and detect it with `if not line.strip():`, and skip `# rescued in May` and detect it with `if line.lstrip().startswith("#"):`.**
3. Write the list of dictionaries a `read_pets` function should return:  
   `Answer:` **[{"name": "Rex", "species": "dog"}, {"name": "Tom", "species": "cat"}]**

> 🤖 **Explain It:** When is `try` / `except` a good idea, and when does it just hide bugs?

**`try` / `except` is a good idea when you expect something might reasonably fail due to external conditions you don’t control. `try` / `except` just hides bugs when it's used to silence errors caused by your own code.**
