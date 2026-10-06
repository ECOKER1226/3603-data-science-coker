# 📝 Worksheet: 03 - Strings and Text

Use this worksheet to reinforce your understanding of strings — creating them, slicing them, cleaning them up, and formatting them. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: String Basics

1. Why doesn't Python care whether you use `'...'` or `"..."`?  
   `Answer:` **Because both create a string**

2. What's the output of this code?

```python
word = 'science'
print(word[0:3])
```

   `Answer:` **sci**

3. Rewrite this string so it could be written with single quotes on the outside instead of double:

```python
message = "She said \"don't stop\""
```

   `Answer:` **'She said "don\'t stop"'**

---

### ✏️ Task: Slicing Practice

```python
# Given: course = "Programming for Data Science"
# Print just the word "Data" using slicing.
# Print the string reversed.

course = "Programming for Data Science"

# Print just "Data"
print(course[17:21])

# Print the string reversed
print(course[::-1])

```

### ✏️ Task: Multi-Line String

```python
# Write a triple-quoted string containing a 3-line "About Me" bio.
# Print it.

bio = """My name is Zeke Coker.
I'm a computer science student at MSU.
I love data science."""
print(bio)
```

### 🤖 Explain It

In your own words: why are strings immutable, and what do you actually have to do if you want a "modified" version of a string?

**Strings are immutable to ensure hashability and safety. If you want a "modified" version of a string, you have to create a new string.**
---

## 🔁 Section 2: String Methods

4. What's the difference between `.strip()` and `.replace(' ', '')`?  
   `Answer:` **.strip() removes whitespace only at the start and end of a string, while .replace(' ', '') removes all whitespaces inside of a string.**

5. What will this print?

```python
name = "  ADA lovelace  "
print(name.strip().title())
```

   `Answer:` **'Ada Lovelace'**

6. If `words = "red,green,blue".split(',')`, what is `words`, and what type is it?  
   `Answer:` **`['red', 'green', 'blue']`, `list`**

---

### ✏️ Task: Clean and Validate

```python
# Given: raw_input = "  YES  "
# Clean it up (strip + lowercase) and check if it equals "yes".
# Print True or False.

raw_input = "  YES  "
clean = raw_input.strip().lower()
print(clean == "yes")
```

### ✏️ Task: Build a Sentence

```python
# Given: words = ['data', 'science', 'is', 'fun']
# Use .join() to turn this into the sentence "data science is fun".
# Then use .replace() to change "fun" to "powerful" in the result.

word = ['data', 'science', 'is', 'fun']
sentence = " ".join(words)
updated = sentence.replace("fun", "powerful")

print(sentence)
print(updated)
```

### 🤖 Explain It

In your own words: what's the difference between a method like `.upper()` that returns a new string, versus a list method like `.append()` that changes the list in place? Why do strings only work the first way?

**.upper() returns a new string because strings are immutable, while .append() changes the list in place because lists are mutable. Strings only work the way to ensure hashability and safety.**
---

## 🎯 Section 3: Formatted Strings

7. What does the format spec `:.2f` do?  
   `Answer:` **It formats a number as a floating-point value rounded to exactly 2 decimal places.**

8. What will this print?

```python
item = "eraser"
qty = 5
print(f"You bought {qty} {item}(s)")
```

   `Answer:` **You bought 5 eraser(s)**

9. Why might you use an f-string instead of `+` to build a string out of variables?  
   `Answer:` **F-strings are clearer, safer, and allow you to embed expressions directly without converting types manually.**

---

### ✏️ Task: Formatted Receipt

```python
# Given: item = "Backpack", price = 45.999, qty = 2
# Print a line like: "2x Backpack @ $46.00 = $92.00"
# (Notice price needs rounding — that's what :.2f is for.)

item = "Backpack"
price = 45.999
qty = 2

print(f"{qty}x {item} @ ${price:.2f} = ${price * qty:.2f}")
```

### ✏️ Task: Aligned Table

```python
# Given: names = ["Ana", "Bartholomew", "Cy"]
# Print each name right-aligned in a 15-character field, one per line,
# so they all line up on the right edge.

names = ["Ana", "Bartholomew", "Cy"]
for n in names:
   print(f"{n:>15}")
```

### 🤖 Explain It

In your own words: what's the practical difference between `f'{price}'` and `f'{price:.2f}'` when `price = 19.999999`? When would the difference actually matter in real code?

**f'{price}' prints 19.999999 while f'{price:.2f}' prints 20.00. The difference would actually matter either when performing precise arithmetic or when formatting must be clean.**
---

## 🚀 Section 4: Going Further (Optional)

These pair with the "🔥 Challenge" sections in the notebooks — skip if you haven't gotten there yet.

### ✏️ Task: Raw String

```python
# Write the Windows path C:\Users\you\Desktop\notes.txt as a raw string.
# Print it, and explain in a comment why the plain (non-raw) version would be risky.

path = r"C:\Users\you\Desktop\notes.txt"
print(path)

# A non-raw string risks interpreting \U or \D as escape sequences, which can cause errors.
```

### ✏️ Task: Debug Format Spec

```python
# Given: width = 10, height = 4
# Use the f'{expr=}' debug spec to print both "width" and "width * height"
# with their values, without writing separate print() calls for each.

width = 10
height = 4

print(f"{width=}, {width * height=}")
```

---

## 🧾 Submit Checklist

- [X] I created strings with single quotes, double quotes, and triple quotes.
- [X] I indexed and sliced a string.
- [X] I used at least three different string methods (`.strip()`, `.split()`, `.join()`, `.replace()`, etc.).
- [X] I built an f-string with more than one embedded expression.
- [X] I used a format spec to control decimal places or alignment.
- [X] I completed the "Explain It" prompts in my own words.
