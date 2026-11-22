# 🎨 Module 08: Visualizing Data

- This module covered how to visualize data, starting with basic `plt.` charts and building up to object-oriented Matplotlib, one-line pandas plots, Seaborn's statistical charts, and the judgment to choose, design, and title a chart so it tells the truth clearly.
- What finally clicked for me in this module was how much easier it is to visualize data with charts over describing data with text and numbers.
- One concept that was worth revisiting was choosing the chart and Seaborn/Pandas function from the question you are asking and the kind of columns you have.
- As for what I would do differently, this module was straightforward and engaging as is, so I wouldn't change anything about it.

---

## 🗂 Notebook Overview

| Notebook | Description |
|----------|-------------|
| [01-Matplotlib_Object_Oriented.ipynb](01-Matplotlib_Object_Oriented.ipynb) | Opens by plotting **Anscombe's quartet**. Then: pyplot vs. `fig, ax`, `ax.set()`, reference lines for Module 07 statistics, **log scales** for skewed data, money/percent tick formatters, `annotate`, `bar_label`, decluttering, multi-panel figures with `sharey` and `layout='constrained'`, `savefig`/`close`, and functions that draw on an `ax`. |
| [02-Plotting_with_Pandas.ipynb](02-Plotting_with_Pandas.ipynb) | `.plot.<kind>()` on Series and DataFrames; turning `value_counts`, `groupby`, `crosstab`, and `pivot_table` straight into charts; sorted vs. ordered bars; grouped and **100% stacked** bars; `ax=` for panels; and **wide vs. long** data with `.melt()`, the bridge to Seaborn. |
| [03-Seaborn_Distributions.ipynb](03-Seaborn_Distributions.ipynb) | Seaborn's column-mapping model, **axes-level vs. figure-level**, `histplot` (`binwidth`, `hue`, `multiple=`, `stat=`, `common_norm=False`), KDE and ECDF plots, the **box plot as the IQR fence rule**, violin and strip plots, and small multiples with `displot(col=, row=)`. |
| [04-Seaborn_Relationships_and_Categories.ipynb](04-Seaborn_Relationships_and_Categories.ipynb) | Scatter plots with `hue`/`style`, overplotting, `regplot`/`lmplot`, the **penguin Simpson's paradox** made visible, Anscombe's identical fitted lines, `countplot` vs. `barplot` vs. `pointplot`, **what error bars mean**, diverging vs. sequential heatmaps, and `pairplot`. |
| [05-Choosing_and_Telling.ipynb](05-Choosing_and_Telling.ipynb) | Choosing a chart from the question and the data types, **honest scales**, ordering categories, color that highlights (colorblind-safe, consistent), **finding titles** and direct labels, a step-by-step **makeover**, and a final checklist. |
| [06-Visualization_Lab.ipynb](06-Visualization_Lab.ipynb) | Capstone lab: turn the Module 07 penguin report into a consistent, titled figure set (distributions, species × sex, island composition, correlations), then build the **paradox figure** and a **one-page summary** yourself. Saves to `06-OutputFiles`. |
