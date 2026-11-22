# 📝 Worksheet: 08 - Visualizing Data

Use this worksheet to reinforce object-oriented Matplotlib, pandas plotting, Seaborn, and chart design. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🖼️ Section 1: Matplotlib, Object-Oriented

1. What's the difference between `plt.title('X')` and `ax.set_title('X')`? When does the difference matter?  
   `Answer:` **plt.title('X') changes the title of the current active axes, while ax.set_title('X') explicitly sets the title for a specific axes object. The difference matters when working with multi-panel figures because ax.set_title() ensures the correct subplot is modified.**

2. You're comparing three histograms in a 1 × 3 figure. Name two settings that make the panels fair to compare.  
   `Answer:` **Use the same bin widths (or bin edges) and shared axes (sharex=True, sharey=True).**

---

### ✏️ Task: A Reusable Chart Function

```python
# Write plot_distribution(ax, series, title, unit) that draws a histogram on ax,
# marks the mean and median with vertical lines, and labels everything.
# Use it to build a 2 x 2 figure of Titanic Age, Fare (log scale!), SibSp, and Parch.
# Save the figure with fig.savefig().

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

def plot_distribution(ax, series, title, unit):
    data = series.dropna()

    ax.hist(data, bins=20, color='steelblue', edgecolor='black')

    mean = data.mean()
    median = data.median()

    ax.axvline(mean, color='red', linestyle='--', label=f'Mean: {mean:.1f}')
    ax.axvline(median, color='green', linestyle='-', label=f'Median: {median:.1f}')

    ax.set_title(title)
    ax.set_xlabel(unit)
    ax.set_ylabel('Count')
    ax.legend()

fig, axes = plt.subplots(2, 2, figsize=(12, 8))

plot_distribution(axes[0, 0], titanic['Age'],
                  'Age Distribution', 'Years')

plot_distribution(axes[0, 1], np.log1p(titanic['Fare']),
                  'Fare Distribution (Log Scale)', 'log(Fare + 1)')

plot_distribution(axes[1, 0], titanic['SibSp'],
                  'Siblings/Spouses Aboard', 'Count')

plot_distribution(axes[1, 1], titanic['Parch'],
                  'Parents/Children Aboard', 'Count')

fig.tight_layout()
fig.savefig('titanic_distributions.png')
```

### 🤖 Explain It

In your own words: why is a function that takes an `ax` argument more useful than a function that calls `plt.` directly?

**A function that takes an ax argument is more useful because it can draw on any subplot or figure. A function that uses plt. directly only works on whichever axes is currently active, making it harder to reuse inside multi-panel figures.**

---

## 🐼 Section 2: Plotting with Pandas

3. When you call `.plot.bar()` on a DataFrame, what does the index become, and what do the columns become?  
   `Answer:` **The index becomes the x-axis categories, and each column becomes a separate bar series (or legend entry).**

4. Give one example of wide data and the same data in long form.  
   `Answer:` **Wide data:**

   **Year | Sales_A | Sales_B**

   **2025 | 100 | 120**

   **2026 | 110 | 135**

   **Long data:**

   **Year | Product | Sales**

   **2025 | A | 100**

   **2025 | B | 120**

   **2026 | A | 110**

   **2026 | B | 135**

---

### ✏️ Task: Summary Table to Chart

```python
# Using pokemon.csv:
# 1. Build a crosstab of Generation vs. Legendary, normalized by row.
# 2. Plot it as a 100% stacked bar chart with a percent-formatted axis.
# 3. Melt the (un-normalized) crosstab into long form with columns Generation, Legendary, count.

poke = pd.read_csv('pokemon.csv')

# Normalized crosstab
ct_norm = pd.crosstab(poke['Generation'], poke['Legendary'], normalize='index')

ax = ct_norm.plot.bar(stacked=True, figsize=(8, 5))

ax.yaxis.set_major_formatter(PercentFormatter(1))
ax.set_ylabel('Percent')
ax.set_title('Legendary Rate by Generation')
plt.tight_layout()

# Un-normalized crosstab
ct = pd.crosstab(poke['Generation'], poke['Legendary'])

# Long form
ct_long = (ct.reset_index().melt(id_vars='Generation', var_name='Legendary', value_name='count'))

print(ct_long.head())
```

### 🤖 Explain It

In your own words: when would you plot with pandas `.plot`, and when would you switch to Seaborn?

**I use pandas .plot() when I've already created a summary table and want a quick chart. I switch to Seaborn when I need grouping, faceting, statistical plots, prettier defaults, or long-format data.**

---

## 🌊 Section 3: Seaborn Distributions

5. Why can a histogram with `hue` and raw counts be misleading when the groups are very different sizes? What's the fix?  
   `Answer:` **Larger groups naturally produce taller bars, even if the shapes of the distributions are similar. Use `stat='density'` or `common_norm=False` to compare shapes fairly.**

6. Explain how a box plot's whiskers and dots connect to the 1.5 × IQR rule from Module 07.  
   `Answer:` **The whiskers extend to the most extreme observations within 1.5 × IQR of the first and third quartiles. Values beyond those limits are plotted individually as outlier dots.**

---

### ✏️ Task: Compare Distributions Four Ways

```python
# Using penguins.csv, for flipper_length_mm by species, make a 2 x 2 figure:
# a step histogram with hue, a KDE with hue, a box plot, and a violin plot.
# Use the same species order and the same colors in every panel.

penguins = pd.read_csv('penguins.csv')

SPECIES_ORDER = ['Adelie', 'Chinstrap', 'Gentoo']
SPECIES_COLORS = dict(zip(['Adelie', 'Chinstrap', 'Gentoo'], sns.color_palette('colorblind', 3)))

fig, axes = plt.subplots(2, 2, figsize=(12, 8))

sns.histplot(data=penguins, x='flipper_length_mm', hue='species', element='step', common_norm=False, palette=SPECIAL_COLORS, ax=axes[0, 0])

sns.kdeplot(data=penguins, x='flipper_length_mm', hue='species'l, common_norm=False, palette=SPECIAL_COLORS, ax=axes[0, 1])

sns.boxplot(data=penguins, x='species', y='flipper_length_mm', order=SPECIES_ORDER, palette=SPECIES_COLORS, ax=axes[1, 0])

sns.violinplot(data=penguins, x='species', y='flipper_length_mm', order=SPECIES_ORDER, palette=SPECIES_COLORS, ax=axes[1, 1])

fig.tight_layout()
plt.show()
```

### 🤖 Explain It

In your own words: the overall penguin body-mass histogram looked like one lumpy pile, and its skew was only 0.47. What did coloring by species reveal, and why couldn't the skew statistic reveal it?

**Coloring by species revealed that the penguins actually consist of separate subpopulations with different centers and spreads. The skew statistic only summarizes the overall distribution with one number, so it cannot reveal distinct clusters hidden inside the data.**

---

## 🔍 Section 4: Seaborn Relationships and Categories

7. What do the error bars on a default `sns.barplot()` mean? How would `errorbar='sd'` change them?  
   `Answer:` **By default, the error bars show a 95% confidence interval around the estimated mean. errorbar='sd' changes them to show plus or minus one standard deviation of the data.**

8. Why should you color a scatter plot by group before adding a trend line?  
   `Answer:` **Different groups may follow different patterns. Coloring first lets you see subgroup relationships and prevents a combined trend line from hiding important differences or producing Simpson's paradox.**

---

### ✏️ Task: Reveal the Paradox

```python
# Using penguins.csv:
# 1. Draw one regplot of bill_length_mm vs. bill_depth_mm for all penguins.
# 2. Draw one regplot per species on a second panel, with r in each label.
# 3. Give each panel a title that states what it shows.

fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# All penguins
sns.regplot(data=penguins, x='bill_length_mm', y='bill_depth_mm', ax=axes[0])

axes[0].set_title('All Penguins Combined')

# By species
for species, color in zip(['Adelie', 'Chinstrap', 'Gentoo'], ['tab:blue', 'tab:orange', 'tab:green']):
    subset = penguins[penguins['species'] == species]

    r = subset['bill_length_mm'].corr(subset['bill_depth_mm'])

    sns.regplot(data=subset, x='bill_length_mm', y='bill_depth_mm', scatter_kws={'alpha': 0.6}, label=f'{species} (r={r:.2f})', color=color, ax=axes[1])

axes[1].set_title('Separate Regression Lines by Species')
axes[1].legend()

plt.tight_layout()
plt.show()
```

### 🤖 Explain It

In your own words: explain Simpson's paradox to someone who has never heard of it, using your chart from the task above.

**Simpson's paradox happens when a trend seen in combined data changes or disappears after splitting the data into meaningful groups. In these penguin measurements, the overall scatterplot suggests one relationship, but once species are separated, each species follows its own pattern. The combined trend is influenced by differences between species rather than only by the relationship within species.**

---

## 🗣️ Section 5: Choosing and Telling

9. Name three things a bar chart's y-axis can do to mislead a reader.  
   `Answer:` **Start above zero, exaggerating differences; Use uneven tick spacing; Use a very narrow or very wide range that distorts visual comparisons.**

10. What's the difference between a descriptive title and a finding title? Write one of each for the same chart.  
    `Answer:` **A descriptive title tells what the chart shows, while a finding title tells the main takeaway. Descriptive title: Median Titanic Fare by Passenger Class. Finding title: First-Class Passengers Paid Much Higher Fares Than Other Classes**

---

### ✏️ Task: Makeover

```python
# Start with: titanic.groupby('Embarked')['Fare'].mean().plot.bar()
# Redesign it with the notebook 05 checklist: the right statistic for skewed data,
# readable port names, sorted bars, a highlight color, bar labels, and a finding title.
# Save the before and after versions.

import matplotlib.pyplot as plt

# BEFORE
ax = titanic.groupby('Embarked')['Fare'].mean().plot.bar()
ax.set_title('Mean Fare by Embarked')
plt.tight_layout()
plt.savefig('fare_before.png')

# AFTER

ports = {'C': 'Cherbourg', 'Q': 'Queenstown', 'S': 'Southampton'}

median_fares = (titanic.groupby('Embarked')['Fare'].median().rename(index=ports).sort_values())

colors = ['lightgray'] * len(median_fares)
colors[-1] = 'crimson'

fig, ax = plt.subplots(figsize=(7, 4))

bars = ax.bar(median_fares.index, median_fares.values, color=colors)

for bar in bars:
    ax.bar_label([bar], fmt='%.2f')

ax.set_ylabel('Median Fare ($)')
ax.set_title('Passengers Embarking at Cherbourg Paid the Highest Typical Fare')

plt.tight_layout()
plt.savefig('fare_after.png')
```

### 🤖 Explain It

In your own words: what's the difference between a chart made for exploration and a chart made for communication? Why do they need different amounts of polish?

**Exploration charts are mainly for helping you discover patterns, so they can be quick and rough. Communication charts are designed for an audience, so they need clear labels, meaningful colors, good titles, annotation, and a focused message. The more a chart is intended to persuade or inform others, the more polish it needs.**

---

## 🧾 Submit Checklist

- [X] I built a multi-panel Matplotlib figure with `fig, ax`, shared axes, and `fig.savefig()`.
- [X] I used a log scale, a reference line, and a tick formatter where they helped.
- [X] I turned a pandas summary table into a chart, and reshaped data between wide and long.
- [X] I compared distributions across groups fairly (`common_norm=False`, shared axes, sample sizes).
- [X] I showed a relationship with a scatter plot colored by group, and explained my error bars.
- [X] I redesigned a default chart using the checklist, with a finding title.
- [X] I completed the "Explain It" prompts in my own words.
