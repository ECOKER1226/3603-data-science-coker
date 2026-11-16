# 📝 Quiz: 07 - Describing Data

36 questions covering types of data, center and spread, shape and outliers, comparing groups, and relationships and correlation. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Types of Data

**1.** (Short Answer) What's the difference between a column's **dtype** and its **measurement scale**?

**Dtype is how the data is stored in pandas (e.g., int, float, object, category). Measurement scale describes what the values mean statistically (nominal, ordinal, interval, ratio).**

**2.** (Multiple Choice) Titanic's `Pclass` is stored as `1`, `2`, `3`. Its measurement scale is:
A) Nominal  **B) Ordinal**  C) Interval  D) Ratio

**3.** (Multiple Choice) Which scale has a true zero that means "none of it"?
A) Nominal  B) Ordinal  C) Interval  **D) Ratio**

**4.** (True/False) Temperature in °C is ratio data, because 20°C is twice 10°C.

**False**

**5.** (Short Answer) Is "number of siblings aboard" discrete or continuous? How can you tell?

**Discrete because it is a count and can only take whole-number values.**

**6.** (Code Tracing) What prints?
```python
s = pd.Series([True, False, True, True])
print(s.mean())
```

**0.75**

**7.** (Short Answer) Why is `titanic['PassengerId'].mean()` meaningless, even though pandas computes it without complaint?

**PassengerId is just an identifier. Averaging IDs produces a number with no real-world interpretation.**

**8.** (Short Answer) What does `ordered=True` in `pd.CategoricalDtype([...], ordered=True)` let you do that a plain `str` column can't?

**It lets pandas recognize and use the category order for comparisons, sorting, min/max, and ordered analyses.**

---

## Section B — Center and Spread

**9.** (Short Answer) Which is more robust to outliers, the mean or the median? Why?

**The median is more robust because extreme values affect it much less than the mean.**

**10.** (Code Tracing) What prints?
```python
s = pd.Series([2, 4, 4, 6, 100])
print(s.median(), s.mode()[0])
```

**4.0 4**

**11.** (Short Answer) A column's mean is much larger than its median. What does that suggest?

**The distribution is likely right-skewed with some large values pulling the mean upward.**

**12.** (Multiple Choice) `pd.Series(data).std()` and `np.std(data)` give slightly different answers because:
A) NumPy rounds  B) pandas skips NaN  **C) they use different default `ddof`**  D) one is variance

**13.** (Short Answer) What's the IQR, and how do you compute it in pandas?

**IQR = Q3 − Q1; iqr = s.quantile(0.75) - s.quantile(0.25)**

**14.** (Short Answer) In `.describe()`, a column's `count` is 714 but the DataFrame has 891 rows. What does that tell you?

**There are 177 missing values in that column.**

**15.** (Short Answer) You fill 177 missing ages with the median age. What happens to the standard deviation, and why?

**Standard deviation usually decreases because replacing many values with the same median reduces variability.**

**16.** (Short Answer) Which spread statistic pairs naturally with the median, and which with the mean?

**IQR pairs naturally with the median, while std pairs naturally with the mean.**

---

## Section C — Shape and Outliers

**17.** (Multiple Choice) A column with `.skew()` of 4.8 is:
A) roughly symmetric  B) strongly left-skewed  **C) strongly right-skewed**  D) heavy-tailed but symmetric

**18.** (Short Answer) Write the formulas for the lower and upper fences of the 1.5 × IQR rule.

**Lower fence = Q1 − 1.5 × IQR; Upper fence = Q3 + 1.5 × IQR**

**19.** (Short Answer) On Titanic fares, the IQR rule flags 116 values but the |z| > 3 rule flags only 20. Why are z-scores less sensitive on a skewed column?

**Large values inflate the mean and standard deviation on a skewed distribution, making z-scores less likely to exceed 3.**

**20.** (True/False) Any value flagged as an outlier should be removed before analysis.

**False**

**21.** (Short Answer) Name two things you can do with a real-but-extreme value instead of deleting it.

**You can transform the data with log transform or cap extreme values.**

**22.** (Short Answer) Why can a value be an outlier within its group but not in the whole dataset (or the other way around)?

**Different groups can have different centers and spreads, so a value may be unusual within its own group but not unusual relative to the whole dataset.**

---

## Section D — Comparing Groups

**23.** (Short Answer) More 3rd-class passengers survived than 2nd-class passengers, but 3rd class had the lower survival rate. How can both be true?

**Because 3rd class had many more passengers. A larger group can have more survivors in total while still having a lower survival rate.**

**24.** (Code Tracing) What does this compute?
```python
titanic.groupby('Sex')['Survived'].mean()
```

**It computes the survival rate for each sex (mean of a 0/1 survival variable).**

**25.** (Multiple Choice) In `pd.crosstab(df['class'], df['Sex'], normalize='index')`, what adds up to 100%?
**A) each row**  B) each column  C) the whole table  D) nothing; it's counts

**26.** (Short Answer) What's the difference between what `pd.crosstab()` and `pivot_table()` compute?

**`pd.crosstab()` primarily computes frequencies or proportions for categories, while `pivot_table()` computes aggregated statistics (mean, sum, count, etc.) of values grouped by categories.**

**27.** (Short Answer) Why should a group summary always include the group's size?

**Small groups can produce unstable or misleading summaries. Sample size provides context for reliability.**

**28.** (Short Answer) Cherbourg passengers survived at a higher rate than other ports. Explain how ticket class could be a **confounder** here.

**If Cherbourg passengers were more likely to travel in higher classes, and higher-class passengers survived more often, part of Cherbourg's higher survival rate may actually be due to ticket class rather than port.**

**29.** (Short Answer) What does `observed=True` do in a `groupby` on a categorical column?

**It only includes category combinations that actually appear in the data, rather than all possible categorical levels.**

---

## Section E — Relationships and Correlation

**30.** (Short Answer) Why is covariance hard to interpret on its own, and how does correlation fix that?

**Covariance depends on the units and scale of the variables, making it hard to interpret. Correlation standardizes covariance to a unitless value between -1 and 1.**

**31.** (Multiple Choice) r = −0.85 means:
A) a weak negative linear relationship  **B) a strong negative linear relationship**  C) 85% of y is caused by x  D) no relationship

**32.** (Short Answer) Give two situations where Spearman is a better choice than Pearson.

**When the relationship is monotonic but not linear or when data is ordinal.**

**33.** (True/False) If r = 0, the two columns have no relationship at all.

**False**

**34.** (Short Answer) Name three explanations for a correlation besides "A causes B."

**B causes A. A third variable causes both (confounding). It's a coincidence.**

**35.** (Short Answer) What is Anscombe's quartet, and what lesson does it teach?

**Anscombe's quartet is four datasets with nearly identical summary statistics (means, variances, correlation, regression line) but very different visual patterns. The lesson is to always visualize your data.**

**36.** (Short Answer) In the penguins data, bill length and depth correlate at −0.24 overall but +0.39 to +0.65 within each species. What's this called, and what causes it here?

**This is Simpson's paradox. Species acts as a confounding variable. Differences between species create an overall negative correlation, while within each species the relationship is positive.**