# 📝 Quiz: 08 - Visualizing Data

36 questions covering object-oriented Matplotlib, plotting with pandas, Seaborn distributions, Seaborn relationships and categories, and choosing and designing charts. Mix of multiple choice, true/false, code-tracing, and short answer.

Try every question on your own first. The Answer Key is at the bottom, no peeking. If you're using an AI tutor, paste in *your answer* and ask it to check your reasoning rather than asking it to solve the question first.

---

## Section A — Matplotlib, Object-Oriented

**1.** (Short Answer) In `fig, ax = plt.subplots()`, what's the difference between `fig` and `ax`?

**fig is the entire figure (the overall canvas). ax is a single set of axes where one chart is drawn.**

**2.** (Short Answer) Why does the object-oriented style scale better than `plt.title()`/`plt.xlabel()` calls when a figure has several charts?

**Because you can explicitly control each subplot with its own ax object, avoiding confusion about which chart is currently active.**

**3.** (Code Tracing) How many axes does this create, and how do you reach the bottom-right one?
```python
fig, axes = plt.subplots(2, 3)
```

**It creates 6 axes arranged in 2 rows and 3 columns. You reach the bottom-right one with `axes[1, 2]`.**

**4.** (Short Answer) What does `sharey=True` do, and why does it matter when comparing panels?

**It makes all subplots use the same y-axis scale, allowing fair visual comparisons between panels.**

**5.** (Short Answer) When is a log-scale axis a good idea? What value can't it show?

**A log scale is useful when values span several orders of magnitude or are highly right-skewed. It cannot show zero or negative values.**

**6.** (Multiple Choice) Which formatter displays `0.25` on an axis as `25%`?
A) `StrMethodFormatter('{x:.0%}')`  **B) `PercentFormatter(xmax=1)`**  C) `PercentFormatter(xmax=100)`  D) `ax.set(percent=True)`

**7.** (Short Answer) Why should you call `fig.savefig()` before `plt.show()`, and why `plt.close(fig)` inside a loop?

**Saving first ensures the figure is written before any backend clears it. `plt.close(fig)` frees memory and prevents figures from accumulating inside loops.**

**8.** (Short Answer) In `ax.annotate('Peak', xy=(5, 10), xytext=(7, 12), arrowprops=...)`, what do `xy` and `xytext` each mean?

**xy is the point being annotated. xytext is where the annotation text is placed.**

---

## Section B — Plotting with Pandas

**9.** (Short Answer) When pandas plots a DataFrame, what becomes the x-axis, and what becomes each line or set of bars?

**The index becomes the x-axis, and each column becomes a separate line or bar series.**

**10.** (Code Tracing) What kind of chart does this draw, and what are the bar labels?
```python
titanic['Embarked'].value_counts().plot.barh()
```

**A horizontal bar chart. The bar labels are the embarkation categories (S, C, and Q).**

**11.** (Short Answer) You plot a `pivot_table` with classes as the index and sexes as the columns. How do you switch the chart to group by sex instead?

**Transpose the table before plotting with `pivot.T.plot(...)`.**

**12.** (Short Answer) What does a 100% stacked bar chart show, and which `crosstab` argument produces the right table for it?

**It shows proportions within each group that add up to 100%. Use `normalize='index'`.**

**13.** (Short Answer) What's the difference between wide and long data? Which does pandas `.plot` expect, and which does Seaborn expect?

**Wide data stores categories in separate columns; long data stores categories in rows with a grouping variable. Pandas `.plot()` generally expects wide data, while Seaborn generally expects long data.**

**14.** (Short Answer) Should you sort the bars of an ordinal category (like ticket class) by value? Why or why not?

**No because ordinal categories have a meaningful order that should be preserved.**

---

## Section C — Seaborn: Distributions

**15.** (Short Answer) What's the difference between an axes-level and a figure-level Seaborn function? Give one example of each.

**Axes-level functions draw onto a specific ax; figure-level functions manage an entire figure and can create multiple panels. Axes-level: `sns.histplot()`. Figure-level: `sns.displot()`.**

**16.** (Short Answer) What does `hue='species'` do in `sns.histplot()`?

**It separates the data into species groups and colors each group differently.**

**17.** (Multiple Choice) Two groups have 500 and 50 rows. To compare the **shapes** of their distributions, use:
A) `stat='count'`  B) `multiple='stack'`  **C) `stat='percent', common_norm=False`**  D) `binwidth=1`

**18.** (Short Answer) Explain each part of a box plot: the box, the line inside it, the whiskers, and the dots.

**Box = IQR (Q1 to Q3); Line inside = median; Whiskers = most extreme values within 1.5 × IQR; Dots = outliers beyond the whiskers**

**19.** (Short Answer) Name one thing a violin plot shows that a box plot hides, and one thing a strip plot shows that a violin hides.

**Violin plot reveals distribution shape and density. Strip plot shows individual observations.**

**20.** (Short Answer) How do you read a group's median from an ECDF plot?

**Find y = 0.50 (50%) and read the corresponding x-value.**

**21.** (True/False) A KDE curve always stays within the actual range of the data.

**False**

**22.** (Short Answer) Why does `showfliers=False` make sense when you draw a strip plot on top of a box plot?

**Because the strip plot already shows every observation, including outliers, so separate outlier dots would be redundant.**

---

## Section D — Seaborn: Relationships and Categories

**23.** (Short Answer) Name two ways to reduce overplotting in a scatter plot.

**Use transparency or smaller markers.**

**24.** (Short Answer) In the penguins data, one `regplot` line through all the points slopes down, but one line per species slopes up. What's this called, and what's the lesson for fitting trend lines?

**This is Simpson's paradox. Always check for meaningful groups before fitting a single trend line to all data.**

**25.** (Short Answer) Why did the four Anscombe datasets get identical lines from `lmplot`?

**Because they share the same summary statistics, including means, variances, correlation, and regression line, despite having very different patterns.**

**26.** (Short Answer) What's the difference between `countplot` and `barplot`?

**`countplot` counts observations in each category. `barplot` computes and plots a summary statistic (usually the mean).**

**27.** (Multiple Choice) `sns.barplot(..., errorbar='sd')` draws error bars showing:
A) the 95% confidence interval  B) the standard error  **C) one standard deviation of the individual values**  D) the IQR

**28.** (Short Answer) What does Seaborn's default error bar on a `barplot` represent?

**A 95% confidence interval around the estimated mean.**

**29.** (Short Answer) What does a `pointplot` with crossing or diverging lines tell you?

**It suggests an interaction effect, meaning the effect of one variable depends on the level of another variable.**

**30.** (Short Answer) Should a correlation heatmap use a diverging or a sequential color map? What about a heatmap of survival rates? Why?

**Correlation heatmap: diverging colormap because values can be positive or negative around a meaningful center (0). Survival-rate heatmap: sequential colormap because values progress from low to high without a midpoint.**

---

## Section E — Choosing and Telling

**31.** (Short Answer) Why must bar charts start at zero, when line charts don't have to?

**Bar lengths encode magnitude from a baseline. Starting above zero exaggerates differences. Line charts emphasize trends and changes, so a nonzero baseline is often acceptable.**

**32.** (Short Answer) Name the chart you'd choose for each: (a) the distribution of one numeric column, (b) the mix of categories within each group, (c) the relationship between two numeric columns.

**(a) Distribution of one numeric column: Histogram**

**(b) Mix of categories within each group: 100% stacked bar chart**

**(c) Relationship between two numeric columns: Scatter plot**

**33.** (Short Answer) What's a palette dictionary, and why use one across a whole report?

**A palette dictionary maps categories to specific colors. Using the same colors consistently helps readers recognize groups across multiple charts.**

**34.** (Short Answer) Rewrite this descriptive title as a finding title: "Mean Body Mass by Species."

**Gentoo penguins have the highest average body mass among the three species.**

**35.** (True/False) Every bar in a bar chart should have its own distinct color.

**False**

**36.** (Short Answer) Give two reasons to look at a chart **and** the matching numbers, rather than just one of them.

**Charts reveal patterns, clusters, outliers, and trends that summary numbers can hide; Numbers provide exact values and prevent misinterpretation of visual impressions.**