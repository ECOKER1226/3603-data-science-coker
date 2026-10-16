# 📂 Module 03b: Containers → Functions

- This module covered Python's built in data containers (lists, tuples, dictionaries, and sets) more thoroughly, the three core patterns of data processing (`Accumulate`, `Count`, `Filter`, and `Best So Far`), and how to create functions and use them to process containers.
- What finally clicked for me in this module was how to identify and when to implement `accumalate`, `count`, `filter`, and `best so far` patterns.
- One concept that was worth revisiting was how to connect small functions into a pipeline.
- As for what I would do differently, this module was straightforward and engaging as is, so I wouldn't change anything about it.

---

## 🔗 Assignments

| Notebook | Description |
|----------|-------------|
| [01-Too_Many_Variables.ipynb](01-Too_Many_Variables.ipynb) | Why lists exist, indexing and `len()` by prediction, tracing a `for` loop by hand, and the three core patterns: **Accumulate**, **Count**, **Filter**. |
| This notebook taught me how to identify and when to implement `accumalate`, `count`, `filter`, and `best so far` patterns. |
| [02-Pick_Your_Container.ipynb](02-Pick_Your_Container.ipynb) | List, tuple, dictionary, and set, each introduced as the fix for a problem. Includes the *Pick Your Weapon* activity and taking nested expressions like `students[1]["grade"]` apart step by step. |
| This notebook taught me that a list is an ordered collection that can change, a tuple is one thing with several fixed parts, a dictionary is a collection of items that can be looked up by name, and a set is an unorderd collection of unique items. |
| [03-Why_Functions.ipynb](03-Why_Functions.ipynb) | From copy/paste to `def`. Defining vs. calling, parameter vs. argument, "a call becomes its return value," and **`print()` vs. `return`**. |
| This notebook taught me to use `print()` when displaying output to the screen and `return` when giving something back to the program. |
| [04-Mystery_Functions.ipynb](04-Mystery_Functions.ipynb) | Read before you write: Predict → Trace → Run → Explain → Modify. One function turned into many variations, a Broken Function Clinic, and Mutation Detective. |
| This notebook taught me how to predict the output of a function by reading the code and identifying its shape (accumulate and return a number, filter and return a list, etc.). |
| [05-Containers_Meet_Functions.ipynb](05-Containers_Meet_Functions.ipynb) | Write the contract first. Rebuild `sum`/`len`/`min`/`max` yourself, then build a toolkit of functions that turn a list into a number, a bool, a list, or a dictionary. Test design. |
| This notebook taught me the four shapes of output (list -> function -> number, True/False, list, or dictionary). |
| [06-Pipelines.ipynb](06-Pipelines.ipynb) | Refactor a blob into small functions and connect them into a pipeline. Includes a pipeline over a list of dictionaries and a team pipeline activity. |
| This notebook taught me how to locate data, identify the shape of the data, decide what needs to happen to the data, tell if that operation can become a function, and what goes in/what comes out of the function. |
