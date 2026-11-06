# 🧰 Module 06: Working with Data (Advanced)

- This module introduced Pandas, the main tool used for manipulating, cleaning, and inspecting data. 
- What finally clicked for me in this module was how much easier and more efficient working with structured data becomes with Pandas.
- One concept that was worth revisiting was choosing between vectorized operations, `.apply()`, and loops.
- As for what I would do differently, this module was straightforward and engaging as is, so I wouldn't change anything about it.

---

## 🗂 Notebook Overview

| Notebook | Description |
|----------|-------------|
| [01-Pandas_Series_and_DataFrames.ipynb](01-Pandas_Series_and_DataFrames.ipynb) | Core Pandas data structures: `Series` (math and filtering on every value at once) and `DataFrame`, built from a dictionary of columns or a list of dictionaries (rows). |
| [02-Loading_and_Exploring_Data.ipynb](02-Loading_and_Exploring_Data.ipynb) | Reading CSVs, dtypes, `.head()`/`.info()`/`.describe()`, duplicates and distinct values, and a first-look checklist ("what does one row represent?"). |
| [03-Indexing_and_Selection.ipynb](03-Indexing_and_Selection.ipynb) | `.loc[]` vs. `.iloc[]` (labels vs. positions), `.set_index()`, `.at[]`/`.iat[]`, boolean masks with `&`/`\|`/`~`, `.isin()`, `.between()`, `.isna()`, rows **and** columns in one `.loc[]`, `.nlargest()`, avoiding chained assignment, and `reset_index()`. |
| [04-Basic_Cleaning.ipynb](04-Basic_Cleaning.ipynb) | What counts as missing, inspecting before cleaning, fill vs. drop (`subset=`, `thresh=`, `ffill`), safe conversions (`format='mixed'` dates, nullable `Int64`), placeholders, text categories, duplicates, and a full cleaning pipeline with validation. |
| [05-Column_Operations.ipynb](05-Column_Operations.ipynb) | Creating columns (arithmetic, True/False, `pd.cut()` bands, `.str`/`.dt`), conditional updates with `.loc[]` (rule order matters), renaming and tidying names, dropping safely, `.apply()` and `apply(axis=1)`, and choosing between vectorized operations, `.apply()`, and loops. |
| [06-Sorting_and_Filtering.ipynb](06-Sorting_and_Filtering.ipynb) | `.sort_values()` (multi-column, returns a copy), named masks for long filters, `.query()` with `in`/`@variables`/backticks, text search with `.str.contains()` (patterns and `regex=False`)/`.startswith()`/`.endswith()`, and filter-then-sort reports. |
| [07-Grouping_and_Combining.ipynb](07-Grouping_and_Combining.ipynb) | `value_counts()` (with percentages), `groupby()` (`.size()` vs. `.count()`, `as_index=False`), named `.agg()`, filtering groups, `pd.concat()` vs. `.merge()`, join types, `suffixes=`, `left_on`/`right_on`, checking joins with `validate=`, and UFO sightings per million people. |
| [08-Pandas_Wrangle_Lab.ipynb](08-Pandas_Wrangle_Lab.ipynb) | Capstone lab: take `messy_purchases.csv` (prices like `$1,249.99`, placeholders, mixed date formats, duplicates, messy names) from raw file to a validated revenue report by state and department — everything above, combined. Saves its results to `08-OutputFiles`. |