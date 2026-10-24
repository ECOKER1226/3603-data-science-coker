# 📝 Quiz: 05 - Foundations

45 questions covering all 8 Foundations notebooks, in order: magic commands, Jupyter workflow, getting help, Markdown, files and paths, data I/O, plotting with NumPy, and timing. Mix of multiple choice, true/false, code-tracing, and short answer.

This is a conceptual self-check. For hands-on practice writing and running real code, see `Foundations_Quiz.ipynb` in this folder.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Magic Commands (01)

**1.** (Multiple Choice) Which magic command shows your current working directory?
**A) `%pwd`**  B) `%cd`  C) `%ls`  D) `%dir`

**2.** (Short Answer) What's the difference between a line magic (`%pwd`), a cell magic (`%%writefile`), and a shell command (`!ls`)?
**A line magic applies to a single line, a cell magic applies to the entire cell, and a shell command runs a command in the system shell.**

**3.** (Code Tracing) A folder contains only `a.csv` and `b.txt`. What kind of value is stored in `files`, and what does it contain?
```python
files = !ls
```
**`files` is a list containing the outpit lines of a shell command.**

**4.** (True/False) `%cd ..  # go up one folder` moves you to the parent folder.
**True**

**5.** (Short Answer) Inside a notebook, why should you install packages with `%pip install` instead of `!pip install`?
**`%pip install` ensures packages install into the same environment the notebook kernel is using.**

**6.** (True/False) `%who` only shows variable *names*, while `%whos` also shows their types and a value summary.
**True**

---

## Section B — Jupyter Workflow (02)

**7.** (Multiple Choice) In Command mode, which keyboard shortcut inserts a new cell *below* the current one?
A) `A`  **B) `B`**  C) `D D`  D) `M`

**8.** (Short Answer) What's the practical difference between Command mode and Edit mode? You press `B` and the letter "b" appears in your code. What happened, and what should you press?
**Command mode allows you to add, delete, and move cells, while Edit mode allows you to type inside a cell. If you press `B` and "b" appears in your code, you're in edit mode and should press `esc` if you want to press `B` to add a new cell below.**

**9.** (Code Tracing) What does this cell display when it runs?
```python
x = 5
x * 2
x * 3
```
**15**

**10.** (Short Answer) A cell near the bottom of a notebook shows `[7]`, and the cell above it shows `[9]`. What does that tell you?
**The cell near the bottom was the 7th cell run and was run before the cell above it, which was the 9th cell run.**

**11.** (True/False) If you delete the cell that created the variable `message`, `message` is removed from memory immediately.
**False**

**12.** (Short Answer) Why should you **Restart & Run All** before submitting a notebook?
**To ensure the notebook runs cleanly, top-to-bottom, with no hidden state.**

---

## Section C — Getting Help (03)

**13.** (Short Answer) `?` shows a docstring. What does `??` sometimes show that `?` doesn't, and why doesn't it always work?
**`??` sometimes show the source code of the object, while `?` only shows the docstring. `??` Doesn't always work because not all built-ins are implemented in Python and some objects are dynamically generated or compiled.**

**14.** (Multiple Choice) The signature is `sorted(iterable, /, *, key=None, reverse=False)`. Which call is valid?
A) `sorted(iterable=nums)`  B) `sorted(nums, None, True)`  **C) `sorted(nums, reverse=True)`**  D) `sorted()`

**15.** (Code Tracing) What error does this raise, and what does it mean?
```python
numbers = [1, 2, 3]
numbers.mean()
```
**AttributeError: `list` object has no attribute `mean`**

**16.** (Short Answer) A long traceback fills the screen. Which line should you read first, and why?
**You should read the last line first because it gives you the actual error type and message.**

**17.** (Short Answer) What does `dir(obj)` give you that Tab completion doesn't?
**`dir(obj)` gives you all attributes, including private ones and magic methods.**

---

## Section D — Markdown (04)

**18.** (Short Answer) What's the Markdown syntax for a level-2 heading (like `## Section 2`)?
**Two hash marks `##`**

**19.** (Short Answer) How do you write **inline** LaTeX math in a Markdown cell, versus a **block** equation on its own line(s)?
**To write inline LaTeX math, weap the text in single dollar signs. To write a block equation on its own line(s), wrap the text in double dollar signs on their own lines.**

**20.** (Short Answer) The Markdown text `The item costs $5 and the tax is $2.` renders strangely. Why, and how do you fix it?
**Markdown interprets `$` as LaTeX math, so $5 and $2 look like math expressions. To fix it, put `\` before the dollar signs.**

**21.** (Short Answer) You typed two lines directly under each other in a Markdown cell, but they render as **one** line. Name two ways to fix it.
**You can fix it by adding two spaces at the end of the first line or by inserting a blank line between them.**

**22.** (Short Answer) Why might you add narrative Markdown cells between code cells instead of just writing code comments?
**Markdown cells let you explain ideas, motivation, and workflow, not just annotate code.**

---

## Section E — Files and Paths (05)

**23.** (Code Tracing) What does this print?
```python
with open('x.txt', 'w', encoding='utf-8') as f:
    f.write('hi')

with open('x.txt', 'r', encoding='utf-8') as f:
    print(f.read())
```
**hi**

**24.** (Multiple Choice) Which file mode adds to the end of an existing file **without** erasing it?
A) `'r'`  B) `'w'`  **C) `'a'`**  D) `'x'`

**25.** (Code Tracing) What does this print?
```python
from pathlib import Path
p = Path('data') / 'sales_2026.csv'
print(p.name, p.stem, p.suffix)
```
**sales_2026.csv sales_2026 .csv**

**26.** (Short Answer) Why is it good practice to use a relative path (like `'data/file.csv'`) instead of an absolute path (like `'C:/Users/yourname/...'`) in a notebook you'll share or submit?
**Absolute paths depend on your machine's username, folder structure, OS, and drive layout, while relative paths work for anyone who has the project folder, regardless of their system.**

**27.** (Code Tracing) `scores.csv` contains the two lines `Name,Score` and `Alice,90`. What does this print, and why might that cause a problem?
```python
import csv
with open('scores.csv', newline='', encoding='utf-8') as f:
    rows = list(csv.reader(f))
print(rows[1])
```
**This prints `['Alice', '90']`, which might cause a problem because CSV readers return strings, not numbers, meaning calculations may not work properly.**

**28.** (True/False) After saving `{'point': (3, 4)}` with `json.dump` and reading it back with `json.load`, you get back exactly the same dictionary.
**False**

---

## Section F — Data Input and Output (06)

**29.** (Short Answer) What does `pd.read_csv('file.csv')` return?
**A DataFrame**

**30.** (Multiple Choice) Which DataFrame method shows summary statistics (mean, standard deviation, min/max, etc.)?
A) `.head()`  B) `.info()`  **C) `.describe()`**  D) `.columns()`

**31.** (Short Answer) You save a DataFrame with `df.to_csv('out.csv')`, read it back, and find an extra `Unnamed: 0` column. What caused it, and how do you prevent it?
**This was caused because the DataFrame was saved with its index, so the index became a column in the CSV. To prevent this, disable index writing with `df.to_csv('out.csv', index=False)`.**

**32.** (Short Answer) What does JSON written with `orient='records'` look like, and why is it usually the layout you want?
**It looks like a list of dictionaries, which matches common web formats, is easy to iterate over, has natural mapping, and works cleanly with Python, JavaScript, and most data pipeline.**

**33.** (Short Answer) After `pd.read_csv`, the ZIP code `02108` shows up as `2108`. Why, and how do you fix it?
**Pandas interprets ZIP codes as integers, stripping leading zeros. To fix this, force the column to be read as a string with `pd.read_csv('file.csv', dtype={'ZIP': str})`.**

**34.** (Short Answer) What does `pd.read_excel('file.xlsx', sheet_name=None)` return?
**A dictionary mapping sheet names to DataFrames**

---

## Section G — Plotting with NumPy and Matplotlib (07)

**35.** (Code Tracing) What do these two lines print?
```python
print([1, 2] * 2)
print(np.array([1, 2]) * 2)
```
**[1, 2, 1, 2] and [2, 4]**

**36.** (Matching) Choose the best chart (line, bar, scatter, or histogram) for each question:
a) Which department sold the most? **bar**
b) How did daily website visits change over a month? **line**
c) Is there a relationship between price and units sold? **scatter**
d) What is the distribution of customer order values? **histogram**

**37.** (Short Answer) A histogram and a bar chart both draw rectangles. What's the difference in what they show?
**A histogram shows the distribution of numeric data by grouping values into bins, while a bar chart compares categories.**

**38.** (Short Answer) You call `plt.show()` and then `plt.savefig('chart.png')`, and the saved image is blank. Why?
**`plt.show()` clears the current figure, so `plt.savefig('chart.png')` saves an empty figure.**

**39.** (Short Answer) On a box plot, what does the line **inside** the box represent, and what do the dots **beyond** the whiskers represent?
**The line inside the box represents the median and dots beyond the wiskers represent outliers.**

---

## Section H — Timing and Performance (08)

**40.** (Short Answer) What's the difference between `%time` and `%timeit`, and why is `%timeit` more trustworthy for comparisons?
**`%time` runs the code once and reports that single timing, while `%timeit` runs the code many times. `%timeit` is more trustworthy for comparisons because it averages over many runs instead of relying on only one run.**

**41.** (Short Answer) Why is a NumPy vectorized operation like `arr ** 2` usually much faster than a Python `for` loop doing the same calculation element by element?
**Because NumPy operations run in optimized C code instead of Python.**

**42.** (True/False) A variable created inside a `%%timeit` cell is available in the cells after it.
**False**

**43.** (Short Answer) What's unfair about comparing `%timeit np.array(my_list) ** 2` against `%timeit arr ** 2` to decide whether squaring is fast?
**`%timeit np.array(my_list) ** 2` includes array creation and squaring, while `%timeit arr ** 2` only includes squaring.**

**44.** (Short Answer) Why is `[s / max(scores) for s in scores]` slow for large lists? How would you fix it, and roughly what happens to its runtime when the list doubles in size?
**It's slow because it recomputes `max(scores` every iteration. To fix it, compute the max once by moving it outside of the loop. The runtime is 4 times slower before the fix, but is only 2 times slower after the fix.**

**45.** (Multiple Choice) What does `%prun` show you?
A) Only the total time of the cell  
**B) How much time was spent in each function called**  
C) How much memory each variable uses  
D) The source code of a function
