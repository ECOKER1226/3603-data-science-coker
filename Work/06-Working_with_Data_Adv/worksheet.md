# 📝 Worksheet: 06 - Working with Data (Advanced)

Use this worksheet to reinforce Pandas Series/DataFrames and the core data-wrangling workflow: load, explore, select, clean, transform, sort/filter/search, group, and combine. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🐼 Section 1: Series and DataFrames

1. What's the difference between a Pandas `Series` and a `DataFrame`? How does a list of dictionaries (from Module 03) turn into one?  
   `Answer:` **A Series is a one-dimensional labeled collection of data, while a DataFrame is a two-dimensional table made up of multiple Series.**

2. If you add two `Series` together and a label appears in only one of them, what value do you get at that label, and why?  
   `Answer:` **You get NaN because Pandas aligns data by labels. If a label exists in only one Series, there is no matching value to add from the other Series.**

---

### ✏️ Task: Series Basics

```python
# Create a Series from a dictionary mapping 4 of your classes to your grade in each.
# Print the Series, then print the average of all grades (hint: .mean()).

import pandas as pd

grades = pd.Series({
    "Python": 95,
    "Database": 88,
    "Math": 92,
    "Networking": 90
})

print(grades)
print("Average:", grades.mean())
```

### 🤖 Explain It

In your own words: how is a Pandas `Series` similar to a Python dictionary, and how is it similar to a list? What does it borrow from each?
**A Pandas Series is similar to a dictionary because each value has a label (index), like a key-value pair. It is also similar to a list because it stores an ordered collection of values that can be accessed and processed together. It combines dictionary-style labels with list-like data storage and operations.**

---

## 📂 Section 2: Loading and Exploring

3. What does `df.info()` tell you that `df.describe()` doesn't?  
   `Answer:` **df.info() shows column data types, number of non-null values, memory usage, and overall structure.**

4. If `df.isnull().sum()` shows `Age: 177`, what does that number mean?  
   `Answer:` **There are 177 missing (NaN) values in the Age column.**

5. In `titanic.csv`, what does **one row** represent, and which column identifies each row?  
   `Answer:` **One row represents a single passenger. The PassengerId column identifies each passenger.**

---

### ✏️ Task: First Look at a Dataset

```python
# Load pokemon.csv.
# Print its shape, its columns, and .describe() for just the numeric columns.
# Which column has the most missing values, if any?

poke = pd.read_csv('pokemon.csv')

print(poke.shape)
print(poke.columns)
print(poke.describe())

# Type 2 has the most missing values
```

### 🤖 Explain It

In your own words: why is it worth running `.info()` and `.isnull().sum()` on a dataset *before* you start analyzing it, rather than jumping straight to the questions you actually care about?

**Running .info() and .isnull().sum() first helps you understand the structure and quality of the data before analysis. You can identify missing values, incorrect data types, and potential problems that could lead to inaccurate results later.**

---

## 🎯 Section 3: Indexing and Selection

6. Rewrite this using `.loc[]` instead of bracket + `.iloc[]` mixed together — or explain why you can't mix them the way it's written:
```python
df.iloc[df['Age'] < 10]  # this is actually broken — why?
```
   `Answer:` **iloc expects integer positions, but df['Age'] < 10 creates a boolean Series. .loc[] accepts boolean masks, so it works correctly.**

7. What's wrong with `df[df['Age'] < 10 and df['Fare'] > 100]`, and how would you fix it?  
   `Answer:` **The Python keyword 'and' cannot compare entire Series objects. You would fix it by using '&' instead.**

8. Rewrite `df[(df['Pclass'] == 1) | (df['Pclass'] == 2)]` with `.isin()`. Why is `.isin()` easier to read when there are five values to match instead of two?  
   `Answer:` **df[df['Pclass'].isin([1, 2])] -> .isin() is easier to read because you can provide a list of values instead of chaining many OR (|) conditions.**

---

### ✏️ Task: Titanic Slicing

```python
# Using titanic.csv:
# 1. Select passengers in 3rd class (Pclass == 3) who survived (Survived == 1).
# 2. Of those, show only the Name, Age, and Fare columns.
# 3. Sort the result by Fare, descending.

result = (
    df.loc[
        (df["Pclass"] == 3) &
        (df["Survived"] == 1),
        ["Name", "Age", "Fare"]
    ]
    .sort_values("Fare", ascending=False)
)

print(result)
```

### 🤖 Explain It

In your own words: why does `df.iloc[df['Age'] < 10]` not work, when `df.loc[df['Age'] < 10]` and `df[df['Age'] < 10]` both do?

**df.iloc[df['Age'] < 10] does not work because .iloc[] uses integer positions, not boolean labels. The expression df['Age'] < 10 produces True/False values. .loc[] and bracket notation are designed to accept boolean masks.**

---

## 🧼 Section 4: Cleaning

9. If a column has the values `['25', 'thirty', '35']`, what happens when you run `pd.to_numeric(col, errors='coerce')` on it?  
   `Answer:` **The values become `[25.0, NaN, 35.0]` because "thirty" cannot be converted**

10. When would you choose `.dropna()` over `.fillna()`, and vice versa?  
   `Answer:` **Use .dropna() when missing rows are few and removing them won't significantly affect the dataset. Use .fillna() when you want to keep the rows and replace missing values with something meaningful such as a mean, median, or placeholder value.**

11. A survey stores missing ages as `-1`. Why is that *worse* for analysis than a blank (`NaN`), and what one-line fix turns them into real missing values?  
   `Answer:` **-1 looks like valid data, so calculations can treat it as a real age and distort results. NaN is recognized as missing data by Pandas. To fix this, use the one-line `df["Age"] = df["Age"].replace(-1, pd.NA)`.**

12. Two rows share an `order_id` but have different amounts. Will `df.drop_duplicates()` remove one? What argument makes it compare only `order_id`?  
   `Answer:` **No. By default, all columns must match. To compare only `order_id`, use `df.drop_duplicates(subset=["order_id"])`.**

---

### ✏️ Task: Clean a Column

```python
# Using ufo.csv:
# 1. Check .isnull().sum() for the whole dataset.
# 2. Pick the column with the most missing values.
# 3. Decide (and justify in a comment) whether dropping or filling makes more
#    sense for that specific column, then do it.

ufo = pd.read_csv('ufo.csv')

print(ufo.isnull().sum())

# 'country' has the most missing values.
ufo[ufo.duplicated(subset=['country'], keep=False)]

# No other column is dependent on 'country', so it should be dropped.
ufo = ufo.drop(columns=['country'])
```

### 🤖 Explain It

In your own words: why might dropping rows with missing data be a bad idea if a large fraction of your dataset has at least one missing value somewhere?

**Dropping rows can remove a large portion of your data if many rows contain at least one missing value. This may reduce sample size, remove important patterns, and potentially bias your results.**

---

## 🧱 Section 5: Column Operations, Sorting, and Filtering

13. What's the difference between `df.rename(columns={'a': 'b'})` and `df.columns = ['b', 'c', 'd']`?  
   `Answer:` **rename() changes only specified column names. Assigning to df.columns replaces the names of all columns and requires exactly the same number of names as columns.**

14. Rewrite this bracket-filter as a `.query()` call:
```python
df[(df['math_score'] >= 80) & (df['science_score'] >= 80)]
```
   `Answer:` **df.query("math_score >= 80 and science_score >= 80")**

15. If `status` is a brand-new column, what do the rows with `score >= 70` contain after `df.loc[df['score'] < 70, 'status'] = 'review'`? How do you give every row a default first?  
   `Answer:` **Rows with scores below 70 contain "review", while rows with `score >= 70` contain NaN. To give every row a default first, use `df["status"] = "pass"` first.**

---

### ✏️ Task: Build a Feature

```python
# Using students.csv:
# 1. Create a "total_score" column (math + science).
# 2. Sort by total_score, descending.
# 3. Print just the top 3 students' first_name and total_score.

df["total_score"] = df["math"] + df["science"]

top3 = (
    df.sort_values("total_score", ascending=False)
      [["first_name", "total_score"]]
      .head(3)
)

print(top3)
```

### ✏️ Task: Loop vs. Vectorized

```python
# Using students.csv:
# 1. Build a list of each student's total score with an .itertuples() loop.
# 2. Compute the same totals with one whole-column expression.
# 3. Confirm they match, then use %timeit to compare the two.

totals_loop = []

for row in df.itertuples():
    totals_loop.append(row.math + row.science)

totals_vectorized = df["math"] + df["science"]

print(totals_loop == totals_vectorized.tolist())

%timeit [row.math + row.science for row in df.itertuples()]
%timeit df["math"] + df["science"]
```

### 🤖 Explain It

In your own words: what does "feature engineering" mean in the context of `total_score` or `average_score` — why create a new column instead of just computing the value fresh every time you need it?

**Feature engineering means creating new information from existing data. A column like total_score combines multiple variables into something more useful. Creating it once makes analysis easier, improves readability, and avoids recalculating the same value repeatedly.**

---

## 🧩 Section 6: Grouping and Combining

16. Describe the three steps of `df.groupby('Pclass')['Survived'].mean()` (split, apply, combine) in plain words. What does the result tell you?  
   `Answer:` **Split rows into groups based on Pclass, apply the mean of Survived within each group, and combine the results as a new Series. The result shows the survival rate for each passenger class.**

17. What's the difference between `pd.concat()` and `.merge()`, and between a `'left'` and an `'inner'` merge?  
   `Answer:` **`pd.concat()` stacks DataFrames together by rows or columns, while `merge()` joins DataFrames based on matching keys. `left` merge keeps all rows from the left table and matching data is added when available, while `inner` merge keeps only rows with matching keys in both tables.**

---

### ✏️ Task: Survival by Group

```python
# Using titanic.csv:
# 1. Find the survival rate by Pclass, then by Pclass AND Sex together.
# 2. Use .agg() to show, per Embarked port: passengers, average Fare, survival rate.
# 3. .reset_index() the result and sort it by survival rate, highest first.

print(df.groupby("Pclass")["Survived"].mean())

print(df.groupby(["Pclass", "Sex"])["Survived"].mean())

result = (
    df.groupby("Embarked")
      .agg(
          passengers=("PassengerId", "count"),
          avg_fare=("Fare", "mean"),
          survival_rate=("Survived", "mean")
      )
      .reset_index()
      .sort_values("survival_rate", ascending=False)
)

print(result)
```

### ✏️ Task: Join Two Tables

```python
# Build a table of 5 students (student_id, name) and a table of 4 grades
# (student_id, grade), where one student has no grade.
# Merge them with how='left' and with how='inner'. How many rows does each give, and why?

import pandas as pd

students = pd.DataFrame({
    "student_id": [1, 2, 3, 4, 5],
    "name": ["Alice", "Bob", "Carol", "Dave", "Emma"]
})

grades = pd.DataFrame({
    "student_id": [1, 2, 3, 4],
    "grade": ["A", "B", "A", "C"]
})

left_merge = students.merge(grades, on="student_id", how="left")
inner_merge = students.merge(grades, on="student_id", how="inner")

print(left_merge)
print(inner_merge)

# The left merge give 5 rows while the inner merge gives 4 rows.
# The left merge keeps every student, including the one without a grade. The inner merge keeps only students who have matching grades.
```

### 🤖 Explain It

In your own words: when you merge UFO sightings (state codes like `'tx'`) with populations (codes like `'TX'`), every state fails to match at first. Why, and what does that teach you about checking keys *before* you join?

**The join fails because 'tx' and 'TX' are different strings. Pandas requires join keys to match exactly. This teaches why you should inspect and clean key columns before merging. Differences in capitalization, spacing, formatting, or data types can cause valid records to fail to match.**

---

## 🧾 Submit Checklist

- [X] I created a `Series` and a `DataFrame` from Python containers (a dictionary or a list of dictionaries).
- [X] I loaded a local CSV into a DataFrame and inspected it with `.info()` and `.describe()`.
- [X] I used both `.loc[]` and `.iloc[]` at least once each.
- [X] I filtered a DataFrame using a compound condition (`&` or `|`).
- [X] I cleaned at least one column with `.fillna()`, `.dropna()`, or `pd.to_numeric()`.
- [X] I created a new column and sorted by it.
- [X] I removed duplicate rows or replaced a placeholder value with `NaN`.
- [X] I filtered with `.isin()`, `.between()`, or `.str.contains()`.
- [X] I used a whole-column (vectorized) calculation instead of a row-by-row loop.
- [X] I summarized groups with `groupby()` (and `.agg()`), and combined tables with `pd.concat()` or `.merge()`.
- [X] I completed the "Explain It" prompts in my own words.
