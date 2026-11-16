# 📝 Worksheet: 07 - Describing Data

Use this worksheet to reinforce the descriptive workflow: what each column means, what's typical, how much it varies, what's unusual, how groups differ, and which columns move together. Each section ends with an **🤖 Explain It** prompt. Write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🏷️ Section 1: Types of Data

1. Classify each as nominal, ordinal, interval, or ratio: `zip code`, `t-shirt size (S/M/L/XL)`, `year of birth`, `monthly rent`.  
   `Answer:` **Nominal, Ordinal, Interval, Ratio**

2. A column has dtype `int64` and only 4 distinct values. Name two things it might really be, and how you'd decide.  
   `Answer:` **It may be a `categorical variable` or a `numeric variable that genuinely only takes a few values`. To decide, inspect the column's meaning, documentation, value labels, and whether arithmetic operations on the values make sense.**

---

### ✏️ Task: Record the Meaning

```python
# Using titanic.csv:
# 1. Convert Embarked to 'category' and map C/Q/S to 'Cherbourg'/'Queenstown'/'Southampton'.
# 2. Create an ordered 'class' column (3rd < 2nd < 1st).
# 3. Print the share of passengers above 3rd class, using a comparison on 'class'.

import pandas as pd

df = pd.read_csv("titanic.csv")

# Embarked as category with labels
df["Embarked"] = (
    df["Embarked"]
      .map({
          "C": "Cherbourg",
          "Q": "Queenstown",
          "S": "Southampton"
      })
      .astype("category")
)

# Ordered passenger class
df["class"] = pd.Categorical(
    df["Pclass"].map({
        3: "3rd",
        2: "2nd",
        1: "1st"
    }),
    categories=["3rd", "2nd", "1st"],
    ordered=True
)

# Share above 3rd class
share_above_3rd = (df["class"] > "3rd").mean()
print(f"Share above 3rd class: {share_above_3rd:.2%}")
```

### 🤖 Explain It

In your own words: why does it matter whether a variable is nominal or ordinal before you compute anything with it? What could go wrong if you averaged an ordinal column's codes?

**Whether a variable is nominal or ordinal determines what calculations are meaningful. Nominal categories are just labels, while ordinal categories have a ranked order. If we average ordinal codes, the result may be misleading because the numeric distances between categories are not necessarily equal.**

---

## 🎯 Section 2: Center and Spread

3. Why is the median usually reported for house prices instead of the mean?  
   `Answer:` **House prices are usually right-skewed, with a few very expensive homes pulling the mean upward. The median is less affected by extreme values and better represents the typical home price.**

4. You compute a standard deviation with pandas and get 14.53, and a classmate uses NumPy and gets 14.52. Who's wrong?  
   `Answer:` **Neither is necessarily wrong. Pandas uses sample standard deviation by default (ddof=1), while NumPy uses population standard deviation by default (ddof=0). The small difference comes from different formulas.**

---

### ✏️ Task: Compare Center and Spread

```python
# Using pokemon.csv:
# For Attack, print the mean, median, std, and IQR.
# Then do the same for Legendary Pokémon only.
# Which group is more spread out, by std and by IQR? Do the two measures agree?

import pandas as pd

df = pd.read_csv("pokemon.csv")

def iqr(series):
    return series.quantile(0.75) - series.quantile(0.25)

# All Pokémon
attack = df["Attack"]

print("All Pokémon")
print("Mean:", attack.mean())
print("Median:", attack.median())
print("Std:", attack.std())
print("IQR:", iqr(attack))

# Legendary only
legendary = df[df["Legendary"] == True]["Attack"]

print("\nLegendary Pokémon")
print("Mean:", legendary.mean())
print("Median:", legendary.median())
print("Std:", legendary.std())
print("IQR:", iqr(legendary))
```

### 🤖 Explain It

In your own words: two classes have the same average exam score, but very different standard deviations. Describe what being a student in each class might be like.

**A class with a small standard deviation has most students earning similar scores close to the average. A class with a large standard deviation has some students doing very well and others struggling, even though the average score is the same.**

---

## 📐 Section 3: Shape and Outliers

5. A column has mean 50, median 38, and `.skew()` of 2.1. Describe its shape.  
   `Answer:` **The distribution is strongly right-skewed.**

6. Name one situation where you **should** remove an outlier, and one where you shouldn't.  
   `Answer:` **You should remove an outlier when the value is clearly a data entry error (age = 500). You shouldn't remove an outlier when the value is unusual but valid (one very expensive house in a house dataset).**

---

### ✏️ Task: Outlier Report

```python
# Using penguins.csv (drop the 2 rows with no measurements first):
# 1. Write or copy iqr_fences(series, k=1.5).
# 2. Count outliers in body_mass_g overall, then within each species.
# 3. Print the flagged rows. Are any of them impossible values?

import pandas as pd

df = pd.read_csv("penguins.csv")
df = df.dropna()

def iqr_fences(series, k=1.5):
    q1 = series.quantile(0.25)
    q3 = series.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - k * iqr
    upper = q3 + k * iqr

    return lower, upper

lower, upper = iqr_fences(df["body_mass_g"])

outliers = df[
    (df["body_mass_g"] < lower) |
    (df["body_mass_g"] > upper)
]

print("Overall outliers:", len(outliers))
print(outliers)

for species, group in df.groupby("species"):
    lo, up = iqr_fences(group["body_mass_g"])
    n = ((group["body_mass_g"] < lo) |
         (group["body_mass_g"] > up)).sum()

    print(species, n)
```

### 🤖 Explain It

In your own words: explain to a classmate why "outlier" and "error" aren't the same thing, using an example from the Titanic fares.

**An outlier is a value that is far from most other values, while an error is an incorrect value. For example, some Titanic passengers paid extremely high fares. Those fares might be outliers because only a few people paid that much, but they are still legitimate values.**

---

## 👥 Section 4: Comparing Groups

7. When should you compare groups with counts, and when with rates?  
   `Answer:` **Use counts when group sizes are similar or when the total number itself matters. Use rates when group sizes differ a lot so comparisons are fair.**

8. What's the difference between `normalize='index'` and `normalize='columns'` in `pd.crosstab()`? Write a question each one answers.  
   `Answer:` **In `normalize='index'`, each row sums to 1. In `normalize='columns'`, each column sums to 1. Question for `normalize='index'`: "Among males, what percentage survived?"; Question for `normalize='columns'`: "Among survivors, what percentage were male?**

---

### ✏️ Task: Survival Table

```python
# Using titanic.csv:
# 1. Bin Age into child (0-12), teen (13-18), adult (19-60), senior (61+) with pd.cut().
# 2. Build a pivot_table of survival rate with age group as rows and Sex as columns.
# 3. Add the group sizes (a second pivot_table with aggfunc='size').
# Which cell has the highest rate? Is its group big enough to trust?

import pandas as pd

df = pd.read_csv("titanic.csv")

df["age_group"] = pd.cut(
    df["Age"],
    bins=[0, 12, 18, 60, float("inf")],
    labels=["child", "teen", "adult", "senior"]
)

survival_rate = pd.pivot_table(
    df,
    values="Survived",
    index="age_group",
    columns="Sex",
    aggfunc="mean"
)

group_sizes = pd.pivot_table(
    df,
    values="Survived",
    index="age_group",
    columns="Sex",
    aggfunc="size"
)

print(survival_rate)
print(group_sizes)
```

### 🤖 Explain It

In your own words: what's a confounder? Describe one in the Titanic data, and how you'd check for it with a table.

**A confounder is a third variable that can make it look like one variable is causing another when it might not be. In the Titanic data, passenger class may confound the relationship between sex and survival because survival rates and the proportion of men and women differed across classes. To check for confounding, compare survival rates within each class using a table or crosstab.**

---

## 🔗 Section 5: Relationships and Correlation

9. When would you use Spearman instead of Pearson?  
   `Answer:` **Use Spearman when the relationship is monotonic but not necessarily linear, when the data are ordinal, or when outliers may heavily affect Pearson correlation.**

10. A news story says "cities with more ice-cream sales have more drownings." Give a likely confounder.  
    `Answer:` **Season is a likely confounder. Hot weather in summer increases both ice-cream sales and swimming activity, which can increase drownings.**

---

### ✏️ Task: Correlation Report

```python
# Using pokemon.csv:
# 1. Compute the Pearson and Spearman correlation matrices of the six stats.
# 2. List the three strongest pairs (use the upper triangle).
# 3. Recompute r(Attack, Defense) for Legendary and non-Legendary separately.

import pandas as pd
import numpy as np

df = pd.read_csv("pokemon.csv")

stats = [
    "HP",
    "Attack",
    "Defense",
    "Sp. Atk",
    "Sp. Def",
    "Speed"
]

pearson = df[stats].corr(method="pearson")
spearman = df[stats].corr(method="spearman")

print("Pearson")
print(pearson)

print("\nSpearman")
print(spearman)

# Three strongest pairs from upper triangle
corr = pearson.abs()

upper = (
    corr.where(
        np.triu(np.ones(corr.shape), k=1).astype(bool)
    )
    .stack()
    .sort_values(ascending=False)
)

print("\nTop 3 pairs:")
print(upper.head(3))

# Attack vs Defense by legendary status
legendary = df[df["Legendary"]]
non_legendary = df[~df["Legendary"]]

print(
    "Legendary:",
    legendary["Attack"].corr(legendary["Defense"])
)

print(
    "Non-Legendary:",
    non_legendary["Attack"].corr(non_legendary["Defense"])
)
```

### 🤖 Explain It

In your own words: Anscombe's four datasets all have r = 0.82. What does that teach you about reporting a correlation without a plot? What's the danger of a single summary number?

**Anscombe's datasets show that two datasets can have the same correlation but completely different patterns. A single summary number like r=0.82 doesn't tell you whether the relationship is linear, curved, or caused by an outlier. That's why it's important to make a plot and not rely only on summary statistics.**

---

## 🧾 Submit Checklist

- [X] I built a data dictionary that separates dtype from measurement scale.
- [X] I used an ordered category and computed a proportion from a boolean column.
- [X] I reported center and spread that fit a column's shape, and explained `ddof`.
- [X] I flagged outliers with the IQR rule, inspected them, and decided what to do with them.
- [X] I compared groups with sizes and rates, using a crosstab and a pivot table.
- [X] I computed Pearson and Spearman correlations and explained a possible confounder.
- [X] I completed the "Explain It" prompts in my own words.
