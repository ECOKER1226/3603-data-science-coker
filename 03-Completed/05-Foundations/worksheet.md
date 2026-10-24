# 📝 Worksheet: 06 - Foundations

Use this worksheet to reinforce the Jupyter/IPython tooling skills from this module. There's one section per notebook, in order. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧙 Section 1: Magic Commands (01)

1. What magic command lists every variable currently in memory, along with its type?  
   `Answer:` **%whos**

2. What's the difference between a line magic (`%pwd`), a cell magic (`%%writefile`), and a shell command (`!ls`)?  
   `Answer:` **A line magic applies to a single line, a cell magic applies to an entire cell, and a shell command runs an operating system command in the shell.**

3. Why does `%cd ..  # go up` fail, and how do you fix it?  
   `Answer:` **%cd does not allow inline comments after the path, so `%cd .. # go up` treats the comment as part of the path. Fix it by putting the comment on a separate line or using `%cd ..` by itself.**

---

### ✏️ Task: Write, Run, and Reload

```python
# Use %%writefile to create tools.py containing a function shout(text)
# that returns text in uppercase with "!" on the end.
# Turn on %load_ext autoreload and %autoreload 2, then import tools and call shout().
# Rewrite tools.py so shout() adds "!!!" instead, and call it again WITHOUT restarting.
```

### 🤖 Explain It

In your own words: why can `!pip install` "succeed" while `import` still fails with `ModuleNotFoundError`? Why does `%pip` avoid the problem?

**!pip install can succeed but still leave import failing because the pip command may install packages into a different Python environment than the one the notebook kernel is using. %pip uses the notebook's current Python interpreter, so the package is installed into the same environment that executes the notebook code.**

---

## ⚡ Section 2: Jupyter Workflow (02)

4. What are the two Jupyter cell modes, and what key switches to each?  
   `Answer:` **Command Mode (press Esc) and Edit Mode (press Enter).**

5. What do the numbers in `[3]`, `[4]`, `[12]` next to code cells tell you, and what *don't* they tell you?  
   `Answer:` **The numbers show the order in which cells were executed. They do not show the order cells appear in the notebook.**

6. A cell's code ends with three expressions on three lines. How many of their values are displayed?  
   `Answer:` **Only the value of the last expression is automatically displayed**

---

### ✏️ Task: Shortcut Drill

```
Using only the keyboard (no mouse):
- Insert 2 new cells below this one.
- Turn one into a Markdown cell and the other into a Code cell.
- Move the Code cell above the Markdown cell.
- Delete the Markdown cell, then undo the deletion.
- Run the Code cell.
```

### ✏️ Task: Break It, Then Fix It

```python
# In three separate cells, IN THIS ORDER, type:
#   print(area)
#   width, height = 4, 5
#   area = width * height
# Get it to work by running cells out of order. Then Restart & Run All,
# watch it fail, and fix the ORDER so it runs top to bottom.
```

### 🤖 Explain It

In your own words, using the "recipe and kitchen" idea: why can a notebook look correct on your screen and still fail for your grader?

**The notebook is like a recipe, but the kernel is the kitchen. The notebook may look correct because ingredients were prepared earlier in a different order. A grader usually starts with a fresh kitchen and follows the recipe from top to bottom. If the recipe depends on work that happened outside that order, it fails.**

---

## 📚 Section 3: Getting Help (03)

7. What's the difference between `help(len)` and `len?`? Which one also works in a plain `.py` script?  
   `Answer:` **`help(len)` displays documentation using Python's built-in help system, while `len?` uses IPython's help feature. `help(len)` also works in a regualr .py script.**

8. In the signature `round(number, ndigits=None)`, which argument is required and which is optional? What's the optional one's default?  
   `Answer:` **`number` is required. `ndigits` is optional and defaults to None.**

9. Name the error type for each: `'5' + 5`, `int('hello')`, `[1, 2][5]`, `{'a': 1}['b']`.  
   `Answer:` **`'5' + 5` -> TypeError; `int('hello')` -> ValueError; `[1, 2][5] -> IndexError; {'a': 1}['b'] -> KeyError**

---

### ✏️ Task: Investigate Without Searching

```python
# Using only ?, Tab/IntelliSense, dir(), and help() (no web searching):
# 1. Find a string method that checks whether a string contains only digits.
# 2. Use a wildcard search (np.*sum*?) to list NumPy functions with "sum" in the name.
# 3. Find out whether np.random.randint's upper limit is included. Prove it with code.
```

### 🤖 Explain It

In your own words: when would you reach for `?` versus `??` versus `help()` versus `dir()` versus the official docs? Is there a natural order you'd try them in?

**You'd usually try:**
1. ? for quick documentation.
2. dir() to discover available methods and attributes.
3. help() for more detailed information.
4. ?? when you want to inspect source code.
5. Official documentation when you need complete explanations, examples, or advanced details.

---

## 📝 Section 4: Markdown (04)

10. What's the difference between `*italic*` and `**bold**` in Markdown?  
    `Answer:` **`*italic*` produces italic text, while `**bold**` produces bold text.**

11. Write the Markdown for a 2-item bulleted list where the second item has its own sub-bullet.  
    `Answer:` 
    - First item
    - Second item
        - Sub-item

12. How do you show a literal price like `$5` in Markdown without it turning into math?  
    `Answer:` **Escape the dollar sign by putting `\` before it.**

---

### ✏️ Task: Mini Report

```markdown
# Write a Markdown cell with:
# - a level-2 heading
# - a short paragraph with a line break in the middle
# - a 3-item list
# - one inline LaTeX expression (try the mean, \bar{x})
# - a small table with a right-aligned number column
```

### 🤖 Explain It

In your own words: what's lost if you write an entire notebook as code + comments only, with no Markdown cells at all? When would *generating* Markdown from code (`display(Markdown(...))`) be better than typing it?

**Without Markdown, a notebook becomes harder to read because the purpose, explanations, conclusions, and organization are missing. Code comments help programmers but are not as visible or structured as Markdown. Generating Markdown from code is useful when reports need to update automatically based on changing data, calculations, or analysis results.**

---

## 📂 Section 5: Files and Paths (05)

13. What does the `with` keyword do when you open a file, and why is it preferred over a plain `open()`/`.close()` pair?  
    `Answer:` **`with` automatically closes the file when the block ends, even if an error occurs. It is safer and cleaner than manually calling `.close()`.**

14. What's the difference between modes `'w'`, `'a'`, and `'x'`?  
    `Answer:` **`w` creates or overwrites a file, `a` appends to the end of a file, and `x` creates a new file and fails if it already exists.**

15. For `Path('reports') / 'final.pdf'`, what are the `.name`, `.stem`, `.suffix`, and `.parent`?  
    `Answer:` **`.name` -> 'final.pdf'; `.stem` -> 'final'; `.suffix` -> '.pdf' -> `.parent` -> Path('reports').**

---

### ✏️ Task: Build, Save, Reload

```python
# Create a dictionary describing yourself (name, major, hobbies as a list).
# Save it to a JSON file with indent=2 (use pathlib to build the path).
# Read it back into a NEW variable and confirm it matches the original with ==.
# Then add a tuple to the dictionary and repeat. Does it still match? Why not?
```

### ✏️ Task: Find Files

```python
# Write three small .txt files into a folder using a loop.
# Use glob('*.txt') to find them WITHOUT typing their names, and print each
# file's name and size in bytes.
```

### 🤖 Explain It

In your own words: why does `csv.reader` give you `'90'` instead of `90`, and why does splitting a CSV line on `','` break on a value like `"Smith, John"`?

**`csv.reader` returns strings because CSV files contain plain text. The reader cannot automatically know whether "90" should be treated as text, an integer, or something else. Splitting on commas fails for values like "Smith, John" because the comma is part of the data. CSV parsers understand quoted fields and therefore know that the comma inside the quotes is not a separator.**

---

## 📊 Section 6: Data Input and Output (06)

16. Name three things `.info()` tells you about a DataFrame that `.head()` doesn't.  
    `Answer:` **Data types (dtype), number of non-null values, and memory usage.**

17. What does `index=False` do in `df.to_csv(...)`, and what happens if you forget it?  
    `Answer:` **index=False prevents Pandas from writing the row index to the CSV. If you forget it, an extra index column is added.**

18. When would you use `pd.json_normalize()` instead of `pd.read_json()`?  
    `Answer:` **Use pd.json_normalize() when JSON contains nested dictionaries or lists that need to be flattened into table columns.**

---

### ✏️ Task: CSV Round Trip

```python
# Create a small DataFrame from a dictionary of lists (use pd.DataFrame(your_dict)).
# Save it to a CSV, then read that CSV back into a new DataFrame.
# Use .equals() to confirm the reloaded DataFrame matches the original.
```

### ✏️ Task: Convert Between Formats

```python
# Take the same DataFrame and save it as JSON (orient='records') and as Excel.
# Read the Excel file back and convert it to a CSV.
# Print the raw text of the JSON and CSV files and compare them.
```

### 🤖 Explain It

In your own words: what information can get lost or changed when converting Excel → CSV, or CSV → DataFrame? Give two examples.

**Information can be lost or changed during conversion. Examples: 1. Excel formatting (colors, fonts, formulas) is lost when saving as CSV. 2. Data types may change when importing CSV into a DataFrame, such as ZIP codes being interpreted as numbers and losing leading zeros.**

---

## 📈 Section 7: Plotting with NumPy (07)

19. What's the difference between `[1, 2, 3] * 2` and `np.array([1, 2, 3]) * 2`?  
    `Answer:` **`[1, 2, 3] * 2` produces `[1, 2, 3, 1, 2, 3]` while `np.array([1, 2, 3]) * 2` produces `array([2, 4, 6])`.**

20. What does `plt.legend()` require in order to show meaningful labels (hint: think about the `plot()` calls before it)?  
    `Answer:` **`plt.legend()` needs plotted data with `label=arguments` (or handles and labels supplied manually).**

21. Which chart would you use for: comparing categories, change over time, a relationship between two numbers, and the distribution of one number?  
    `Answer:` **Comparing categories -> Bar chart; Change over time -> Line chart; Relationship between two numbers -> Scatter plot; Distribution of one number -> Histogram.**

---

### ✏️ Task: Compare Three Categories

```python
# Given: subjects = ["Math", "Science", "History"]
#        hours_studied = [5, 8, 3]
# Build a bar plot with a title and axis labels (with units).
# Save it to a PNG file, then display it.
```

### ✏️ Task: Distribution

```python
# Generate 200 test scores with np.random.normal(75, 10, size=200).
# Plot a histogram and mark the mean with a vertical dashed line and a legend.
# Then show the same data as a box plot side by side, using subplots.
```

### 🤖 Explain It

In your own words: why does a line plot make sense for `sin(x)` or monthly revenue but not for the categories `"Math"`, `"Science"`, `"History"`? What's different about the two kinds of data?

**Line plots work for data with an order or continuous progression, such as time or numeric x-values like sin(x). Connecting points makes sense because values exist between the plotted points. Categories like "Math", "Science", and "History are separate labels with no continuous relationship between them. Connecting them with lines wrongly suggests a trend or progression, so a bar chart is more appropriate.**

---

## ⏱️ Section 8: Timing and Performance (08)

22. What's the difference between `%time`, `%timeit`, `%%time`, and `%%timeit`?  
    `Answer:` **`%time` times on line once, `%timeit` runs one line many times and reports statistics, `%%time` times an entire cell once, and `%%timeit` runs an entire cell many times and reports statistics.**

23. Name two things that make a timing comparison **unfair**.  
    `Answer:` **Timing different amounts of work and including setup work in one version but not the other.**

24. What does `%prun` tell you that `%timeit` doesn't?  
    `Answer:` **`%prun` shows where time is spent inside function calls, while `%timeit` only reports overall execution speed.**

---

### ✏️ Task: Timing Comparison

```python
# Build a list of the first 500,000 integers, and a NumPy array of the same.
# Use %timeit -o to compare squaring the list with a comprehension
# vs. squaring the array (numbers ** 2).
# Confirm both give the same values, then print how many times faster NumPy is.
```

### ✏️ Task: Find the Repeated Work

```python
# This function is slow. Time it, find the repeated work, fix it, and time it again:
def above_average(values):
    return [v for v in values if v > sum(values) / len(values)]
```

### 🤖 Explain It

In your own words: why does `%timeit` run your code many times instead of just once like `%time`? And why should you "measure first" instead of rewriting code that just *looks* slow?

**`%timeit` runs code many times because a single run may be affected by background processes, caching, or random system activity. Multiple runs produce a more reliable average. You should measure first because code that looks slow may not actually be slow. Profiling identifies real performance problems so you don't waste time optimizing code that already runs fast enough.**

---

## 🧾 Submit Checklist

- [X] I used at least 3 different magic commands, including one cell magic and one `!` shell command.
- [X] I fixed a notebook that only worked when run out of order, and I can explain why it failed.
- [X] I ran **Restart & Run All** on my notebooks before submitting.
- [X] I used `?`, `help()`, or `dir()` to look something up instead of guessing.
- [X] I wrote a Markdown cell with a heading, a list, a table, and LaTeX math.
- [X] I wrote and read back a text file, a JSON file, and a CSV file using `pathlib` paths.
- [X] I loaded data with Pandas and converted it between at least two formats.
- [X] I built at least one plot with a title, axis labels, and (if applicable) a legend, and saved it to a file.
- [X] I timed two approaches fairly with `%timeit`.
- [X] I uploaded each notebook's `NN-OutputFiles` folder along with the notebook.
- [X] I completed the "Explain It" prompts in my own words.
