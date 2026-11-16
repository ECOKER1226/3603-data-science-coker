# 🔢 Module 07: Describing Data

- This module covered types of data (qualitative/quantitative, discrete/continuous, the four scales (nominal, ordinal, interval, ratio)), center and spread, shape and outliers, comparing groups, and relationships and correlation. These concepts show how to figure out what each column means, what's typical, how much things vary, which values are unusual, how groups differ, and which columns move together.
- What finally clicked for me in this module was the fact that correlation is not causation, for a confounder may play a role or the correlation may be a coincidence.
- One concept that was worth revisiting was knowing how to identify confounders and how they distort data.
- As for what I would do differently, this module was straightforward and engaging as is, so I wouldn't change anything about it.

---

## 🗂 Notebook Overview

| Notebook | Description |
|----------|-------------|
| [01-Types_of_Data.ipynb](01-Types_of_Data.ipynb) | **dtype vs. meaning**: qualitative/quantitative, discrete/continuous, the four scales (nominal, ordinal, interval, ratio), recording meaning with `category`, ordered `CategoricalDtype`, and `bool`, why the mean of a True/False column is a proportion, and building a **data dictionary**. Saves to `01-OutputFiles`. |
| [02-Center_and_Spread.ipynb](02-Center_and_Spread.ipynb) | `.mean()`/`.median()`/`.mode()` and robustness, range/variance/std, `ddof` (why pandas and NumPy disagree), percentiles and the IQR, reading `.describe()` row by row, summarizing text columns, and how filling missing values shrinks the spread. |
| [03-Shape_and_Outliers.ipynb](03-Shape_and_Outliers.ipynb) | Symmetric vs. skewed, `.skew()` and `.kurt()`, the **1.5 × IQR** fence rule (as a reusable function), z-scores and why they fail on skewed data, inspecting before deciding, log transforms, and capping with `.clip()`. |
| [04-Comparing_Groups.ipynb](04-Comparing_Groups.ipynb) | Group summaries with size + center + spread, **rates not counts**, `pd.crosstab()` with `normalize=`, `pivot_table()`, groups from `pd.cut()`, and two traps: tiny groups and **confounders**. |
| [05-Relationships_and_Correlation.ipynb](05-Relationships_and_Correlation.ipynb) | Covariance vs. correlation, `.corr()` for a pair or a matrix, listing the strongest pairs, **Pearson vs. Spearman**, why r ≈ 0 doesn't mean "no relationship," correlation vs. causation, and **Anscombe's quartet**. |
| [06-Describing_Data_Lab.ipynb](06-Describing_Data_Lab.ipynb) | Capstone lab: describe the Palmer Penguins dataset from raw file to saved report: clean, data dictionary, summaries, outliers overall vs. within species, species comparisons, and a **Simpson's paradox** in the bill measurements. Saves to `06-OutputFiles`. |