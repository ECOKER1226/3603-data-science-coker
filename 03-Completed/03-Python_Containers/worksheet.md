# 📝 Worksheet: 01 - Working with Data

Use this worksheet to review and reinforce your understanding of Python's core data containers. Each section ends with an **🤖 Explain It** prompt — write your explanation in your own words, then (optionally) paste it into an AI tutor and ask it to point out anything you got wrong or left out.

---

## 🧠 Section 1: Lists

1. What method adds an item to the end of a list?  
   `Answer:` **.append()**

2. How can you remove an item from a list by value? By position?  
   `Answer:` **By value: .remove(value); By position: .pop(index)**

3. What's the result of this code?

```python
nums = [2, 4, 6]
nums.append(8)
print(nums)
```

   `Answer:` **[2, 4, 6, 8]**

4. What does `my_list[1:4]` return, given `my_list = [10, 20, 30, 40, 50]`?  
   `Answer:` **[20, 30, 40]**

4a. Given `a = [1, 2]` and `b = [3, 4]`, what is the result of `a + b`? Of `a.append(b)`? Of `a.extend(b)`?  
   `Answer:` **a + b: [1, 2, 3, 4]; a.append(b): [1, 2, [3, 4]]; a.extend(b): [1, 2, 3, 4]**

4b. Given `grid = [[1, 2], [3, 4]]`, how do you access the value `3`?  
   `Answer:` **print(grid[1][0])**

4c. List three different ways to remove an item from a list.  
   `Answer:` **.remove(value), .pop(index), and del mylist[index]**

---

### ✏️ Task: List Practice

```python
# Create a list of your top 3 favorite foods.
# Add another food to the list.
# Remove one item and print the list.

food = ["burgers", "hot dogs", "pizza"]
food.append("apples")
food.remove("hot dogs")
print(food)
```

### ✏️ Task: Slicing and Sorting

```python
# Given: numbers = [42, 17, 8, 99, 23, 4]
# 1. Print the first three numbers using slicing.
# 2. Print the numbers sorted from smallest to largest.
# 3. Print the numbers sorted from largest to smallest.

numbers [42, 17, 8, 99, 23, 4]
print(numbers[0:3])
print(sorted(numbers))
print(sorted(numbers)[::-1])
```

### ✏️ Task: Filtering

```python
# Given: temps = [55, 72, 90, 43, 88, 67, 101]
# Build a new list called "hot" containing only temps over 85.
# Print "hot".

temps = [55, 72, 90, 43, 88, 67, 101]
hot = []
for temp in temps:
   if temp > 85:
      hot.append(temp)

print(hot)
```

### ✏️ Task: Combine Lists Three Ways

```python
# Given: morning = ['eggs', 'toast']
#        extras  = ['jam', 'coffee']
# 1. Use + to make a new list "breakfast" without changing "morning".
# 2. On a fresh copy of "morning", use .append(extras) and print the result.
#    Notice how many items the list has now, and why.
# 3. On another fresh copy, use .extend(extras) and print the result.

morning = ['eggs', 'toast']
extras = ['jam', 'coffee']
breakfast = morning + extras

morning = ['eggs', 'toast']
extras = ['jam', 'coffee']
print(morning.append(extras))

morning = ['eggs', 'toast']
extras = ['jam', 'coffee']
print(morning.extend(extras))
```

### ✏️ Task: 2D List (grid)

```python
# board = [
#     [1, 2, 3],
#     [4, 5, 6],
#     [7, 8, 9],
# ]
# 1. Print the value in row 2, column 0.
# 2. Change the center value to 0.
# 3. Loop over the board and print each row on its own line.

board = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
]

print(board[2][0])

board[1][1] = 0

for b in board:
   print(b)
```

### ✏️ Task: Deleting Items

```python
# Given: queue = ['Ana', 'Ben', 'Cy', 'Dana', 'Eve']
# 1. Remove 'Cy' by value.
# 2. Use .pop() to remove and capture the last person into a variable "served".
# 3. Use del to remove the first person.
# 4. Print the remaining queue and "served".

queue = ['Ana', 'Ben', 'Cy', 'Dana', 'Eve']
queue.remove('Cy')
served = queue.pop(-1)
del queue[0]
print(queue, served)
```

### ✏️ Task: Iterate by Index

```python
# Given: prices = [10, 20, 30, 40]
# 1. Use "for i in range(len(prices)):" to print each item as "0: 10", "1: 20", ...
# 2. Using the index, add 5 to every price in place, then print the list.
# 3. Rewrite step 1 using enumerate() instead.

prices = [10, 20, 30, 40]
for i in range(len(prices)):
   index = 0
   print("{index}: {i}\n")
   index += 1
   i += 1
```

### 🤖 Explain It

In your own words: what's the difference between a list and a slice of a list? Is slicing a list the same as modifying it? And when you write `a.append(b)` versus `a.extend(b)`, what ends up in `a` each way?

**A list is the actual data structure that holds elements, while a slice of a list is a new list created by copying a portion of the original. Slicing a list is not the same as modifying it. When you write 'a.append(b)', The entire list 'b' becomes one element inside 'a'. When you write 'a.extend(b)', the elements of 'b' are added rather than 'b' itself.**

---

## 🔒 Section 2: Tuples

5. What is a key difference between a list and a tuple?  
   `Answer:` **A list is mutable while a tuple is immutable**

6. Can you change the contents of a tuple once it is created? Why or why not?  
   `Answer:` **No because tuples are immutable, which makes them hashable**

7. What does `first, *rest = (10, 20, 30, 40)` assign to `first` and `rest`?  
   `Answer:` **first = 10; rest = [20, 30, 40]**

---

### ✏️ Task: Tuple Practice

```python
# Create a tuple with your favorite 3 numbers.
# Unpack it into three variables and print each.

nums = (7, 42, 108)
a, b, c = nums
print(a)
print(b)
print(c)
```

### ✏️ Task: Unpacking with *rest

```python
# Given: race_times = (9.58, 9.63, 9.69, 9.71, 9.74)
# Unpack this into "winner" (the first time) and "others" (everything else).
# Print both.

race_times = (9.58, 9.63, 9.69, 9.71, 9.74)
winner, *others = race_times
print("winner:", winner)
print("others:", others)
```

### ✏️ Task: Tuples as Dictionary Keys

```python
# Build a dictionary called "distances" where the keys are (city1, city2)
# tuples and the values are the distance in miles between them.
# Add at least two entries, then look up and print one of them.

distances = {
   ("Dallas", "Austin"): 195,
   ("Houston", "San Antonio"): 197
}
```

### 🤖 Explain It

In your own words: why does Python allow a tuple to be a dictionary key, but not a list? What property makes that possible?

**Python allows a tuple to be a dictionary key because tuples are immutable and therefore hashable. Python does not allow a list to be a dictionary key because lists are mutable and therefore unhashable.**

---

## 🔑 Section 3: Dictionaries

8. What does the `.get()` method do differently from accessing a key directly with `[]`?  
   `Answer:` **Using [] requires that the key exist, while .get() will just return None if the key doesn't exist.**

9. How do you loop through both keys and values in a dictionary?  
   `Answer:` **You loop through both keys and values by using the dictionary's .items() method.**

10. How would you remove a key from a dictionary and also capture the value it held?  
    `Answer:` **The best way to remove a key and capture its value at the same time is to use .pop()**

11. In a list of dictionaries like `people = [{'name': 'Ana'}, {'name': 'Ben'}]`, how do you get Ben's name?  
    `Answer:` **You index into the list first, then into the dictionary: print(people[1]['name']**

12. If the same dictionary object is stored in both a list and another dictionary, and you change it through one, does the other see the change? Why?  
    `Answer:` **Yes because lists and dictionaries store references to objects, not copies.**

---

### ✏️ Task: Dictionary Practice

```python
# Create a dictionary with keys: 'name', 'age', and 'hobby'.
# Print each key and value in the format "key: value".

person = {
   "name": "Ana",
   "age": 28,
   "hobby": "painting"
}

for key, value in person.items():
   print(f"{key}: {value}")
```

### ✏️ Task: Build from Two Lists

```python
# Given: products = ['pen', 'notebook', 'eraser']
#        prices = [1.50, 3.25, 0.75]
# Build a dictionary mapping each product to its price.
# Print the total cost of all products (hint: sum the .values()).

products = ['pen', 'notebook', 'eraser']
prices = [1.50, 3.25, 0.75]

product_prices = dict(zip(products, prices))

total = sum(product_prices.values())
print("Total cost:", total)
```

### ✏️ Task: Nested Dictionaries

```python
# Given:
# inventory = {
#     'apples': {'count': 50, 'price': 0.50},
#     'bananas': {'count': 30, 'price': 0.25},
# }
# Loop through inventory and print a line for each fruit like:
# "apples: 50 units at $0.50"

inventory = {
   'apples': {'count': 50, 'price': 0.50},
   'bananas': {'count': 30, 'price': 0.25},
}

for fruit, info in inventory.items():
   count = info['count']
   price = info['price']
   print(f"{fruit}: {count} units at ${price:.2f}")
```

### ✏️ Task: List of Dictionaries (table rows)

```python
# roster = [
#     {'name': 'Alex', 'major': 'CS'},
#     {'name': 'Ana',  'major': 'Math'},
#     {'name': 'Ben',  'major': 'History'},
# ]
# 1. Loop over roster and print "name - major" for each student.
# 2. Add a new student record to the list.
# 3. Build and print a list of just the names of everyone majoring in 'CS'.

roster = [
    {'name': 'Alex', 'major': 'CS'},
    {'name': 'Ana',  'major': 'Math'},
    {'name': 'Ben',  'major': 'History'},
]

for student in roster:
   print(f"{student['name']} - {student['major']}")

roster.append({'name': 'Cara', 'major': 'CS'})

cs_students = [student['name'] for student in roster if student['major'] == 'CS']

print(cs_students)
```

### ✏️ Task: Update a Record by Row Number

```python
# Using the roster above:
# 1. Build a dict "by_row" mapping each row number to its record
#    (hint: {i: row for i, row in enumerate(roster)}).
# 2. Change the major of the student in row 2 to 'CS'.
# 3. Print roster[2] and explain why it changed too.

roster = [
    {'name': 'Alex', 'major': 'CS'},
    {'name': 'Ana',  'major': 'Math'},
    {'name': 'Ben',  'major': 'History'},
]

by_row = {i: row for i, row in enumerate(roster)}
by_row[2]['major'] = 'CS'
print(roster[2])
```

### 🤖 Explain It

In your own words: what's the difference between `student['gpa']` and `student.get('gpa')` when `'gpa'` isn't in the dictionary? Which would you use, and when? Also: why does changing `by_row[2]` also change `roster[2]`?

**`student['gpa']` tries to access the key directly. If 'gpa' is missing, Python raises a KeyError. `student.get('gpa')` Safely returns the value if the key exists. If the key is missing, returns None or a default. Use `student['gpa']` when the key is required and missing it should stop the program. Use `student.get('gpa')` when the key is optional, uncertain or want a default value. Changing `by_row[2]` also changes `roster[2]` because `by_row[2]` is a reference to `roster[2]`, not a copy.**

---

## 🚀 Section 4: Going Further (Optional)

These pair with the "🔥 Challenge" sections in the notebooks — skip if you haven't gotten there yet.

### ✏️ Task: List Comprehension

```python
# Rewrite this loop as a one-line list comprehension:
# cubes = []
# for n in range(6):
#     cubes.append(n ** 3)

cubes = [n**3 for n in range(6)]
```

### ✏️ Task: namedtuple

```python
# Create a namedtuple called "Book" with fields "title" and "author".
# Make one instance and print both fields by name.

from collections import namedtuple

Book = namedtuple("Book", ["title", "author"])

b = Book(title="The Road", author="Cormac McCarthy")

print(b.title)
print(b.author)
```

### ✏️ Task: Word Counter

```python
# text = "to be or not to be that is the question"
# Build a dictionary counting how many times each word appears.
# (Try it by hand first, then check yourself with collections.Counter.)

text = "to be or not to be that is the question"

counts = {}
for word in text.split():
   if word in counts:
      counts[word] += 1
   else:
      counts[word] = 1

print(counts)

from collections import Counter

print(Counter(text.split()))
```

### ✏️ Task: Parse Some JSON

```python
import json
raw = '''
{
  "course": "Programming for Data Science",
  "online": true,
  "instructor": null,
  "students": [
    {"name": "Alex", "grade": 91},
    {"name": "Ana",  "grade": 88}
  ]
}
'''
# 1. Use json.loads(raw) to turn this into Python objects.
# 2. Print the course name and the second student's grade.
# 3. Print the Python type of the value that came from "online" and from "instructor".

import json

data = json.loads(raw)

print(data["course"])
print(data["students"][1]["grade"])

print(type(data["online"]))
print(type(data["instructor"]))
```

### ✏️ Task: Walk a GeoJSON FeatureCollection

```python
geo = {
    "type": "FeatureCollection",
    "features": [
        {"type": "Feature",
         "geometry": {"type": "Point", "coordinates": [-98.529, 33.878]},
         "properties": {"name": "Bolin Hall"}},
        {"type": "Feature",
         "geometry": {"type": "Point", "coordinates": [-98.531, 33.876]},
         "properties": {"name": "Moffett Library"}},
    ],
}
# Loop over geo["features"] and print each building's name with its
# latitude and longitude. Remember: coordinates are [longitude, latitude].

for feature in geo["features"]:
   name: feature["properties"]["name"]
   lon, lat = feature["geometry"]["coordinates"]
   print(f"{name}: latitude {lat}, longitude {lon}")
```

---

## 🧾 Submit Checklist

- [X] I practiced creating, slicing, sorting, and filtering lists.
- [X] I can explain the difference between `+`, `append()`, and `extend()`.
- [X] I built and traversed a nested (2D) list.
- [X] I removed list items with `remove()`, `pop()`, and `del`.
- [X] I looped by index with `range(len(...))` and with `enumerate()`.
- [X] I understand how tuples are different from lists, and why that makes them hashable.
- [X] I accessed, looped through, updated, and removed items from a dictionary.
- [X] I built a dictionary from two separate lists.
- [X] I worked with at least one nested dictionary.
- [X] I processed a list of dictionaries as table rows and updated a record by row number.
- [X] I parsed JSON with `json.loads()` and walked a GeoJSON FeatureCollection.
- [X] I completed the "Explain It" prompts in my own words.
