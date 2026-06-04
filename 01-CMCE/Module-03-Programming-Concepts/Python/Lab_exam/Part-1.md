# 🐍 Python Exam Prep — Part 1: Data Structures

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Topics](https://img.shields.io/badge/Topics-5-green)
![Questions](https://img.shields.io/badge/Questions-75-orange)
![Level](https://img.shields.io/badge/Level-Basic%20to%20Medium-yellow)

---

## 📌 Index

| # | Topic | Questions |
|---|---|---|
| 1 | [📘 Dictionaries](#-topic-1-dictionaries) | Q1–Q15 |
| 2 | [📘 Lists](#-topic-2-lists) | Q1–Q15 |
| 3 | [📘 Tuples](#-topic-3-tuples) | Q1–Q15 |
| 4 | [📘 Sets](#-topic-4-sets) | Q1–Q15 |
| 5 | [📘 Strings](#-topic-5-strings) | Q1–Q15 |

---

## 🗺️ Legend

| Symbol | Meaning |
|---|---|
| 🟢 | Understanding — Concept/Output based |
| 🔵 | Basic Programs — 2–5 lines, single concept |
| 🟡 | Medium Programs — 10–20 lines, multi-concept |
| ✅ | Guided Solution |
| 💡 | Key Tip |

---

## 📘 Topic 1: Dictionaries

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `d = {}` | Create empty dictionary |
| `d = {'key': value}` | Create dictionary with values |
| `d['key']` | Access value by key |
| `d.get('key')` | Safe access (returns None if not found) |
| `d['key'] = value` | Add or update key |
| `del d['key']` | Delete a key |
| `d.keys()` | Get all keys |
| `d.values()` | Get all values |
| `d.items()` | Get all key-value pairs |
| `'key' in d` | Check if key exists |
| `d.update({})` | Merge another dict into d |
| `d.pop('key')` | Remove and return value |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a dictionary in Python? What makes it different from a list?**

✅ **Answer:**
- A dictionary stores data as **key-value pairs**.
- A list stores data as **ordered indexed elements**.
- Dictionary keys must be **unique and immutable** (string, int, tuple).
- Lists use **integer indices (0, 1, 2...)**, dictionaries use **custom keys**.

```python
# List
fruits = ['apple', 'banana', 'cherry']
print(fruits[0])  # apple

# Dictionary
fruit_color = {'apple': 'red', 'banana': 'yellow'}
print(fruit_color['apple'])  # red
```

💡 **Key Tip:** Dictionaries are unordered in Python < 3.7, ordered by insertion in Python ≥ 3.7.

---

**Q2. What is the output of the following code?**

```python
d = {'name': 'Alice', 'age': 25, 'city': 'Pune'}
print(d['age'])
print(d.get('country'))
print(d.get('country', 'Not Found'))
```

✅ **Answer:**
```
25
None
Not Found
```

💡 **Key Tip:** `.get()` never raises a `KeyError`. If key is missing, it returns `None` or the default value you provide.

---

**Q3. True or False — with reason.**

```
a) Dictionary keys can be a list.
b) Dictionary values can be duplicated.
c) d.keys() returns a list.
d) You can have two identical keys in one dictionary.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Keys can be a list | ❌ False | Keys must be **immutable**; lists are mutable |
| b) Values can be duplicated | ✅ True | Only keys must be unique, not values |
| c) `d.keys()` returns a list | ❌ False | It returns a `dict_keys` view object |
| d) Two identical keys allowed | ❌ False | Duplicate keys — later one **overwrites** earlier |

---

**Q4. Fill in the blank to complete the code.**

```python
student = {'name': 'Bob', 'grade': 'A'}

# Add a new key 'age' with value 20
student[______] = ______

# Delete the key 'grade'
del student[______]

# Print all keys
print(student.______())
```

✅ **Answer:**
```python
student['age'] = 20
del student['grade']
print(student.keys())
```

**Output:**
```
dict_keys(['name', 'age'])
```

---

**Q5. What is the output?**

```python
d = {'a': 10, 'b': 20, 'c': 30}

for key, value in d.items():
    print(f"{key} → {value}")

print('b' in d)
print('z' in d)
```

✅ **Answer:**
```
a → 10
b → 20
c → 30
True
False
```

💡 **Key Tip:** `in` on a dictionary checks for **keys only**, not values.

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Create a dictionary of 3 students with their marks. Print each student's name and marks.**

✅ **Solution:**
```python
# Dictionary: student name → marks
students = {
    'Alice': 88,
    'Bob': 75,
    'Charlie': 92
}

# Loop through and print
for name, marks in students.items():
    print(f"Student: {name} | Marks: {marks}")
```

**Output:**
```
Student: Alice | Marks: 88
Student: Bob | Marks: 75
Student: Charlie | Marks: 92
```

---

**Q7. Write a program to add a new key-value pair to an existing dictionary and then delete one key.**

✅ **Solution:**
```python
car = {'brand': 'Toyota', 'model': 'Camry', 'year': 2020}

# Add new key
car['color'] = 'Blue'
print("After adding:", car)

# Delete a key
del car['year']
print("After deleting:", car)
```

**Output:**
```
After adding: {'brand': 'Toyota', 'model': 'Camry', 'year': 2020, 'color': 'Blue'}
After deleting: {'brand': 'Toyota', 'model': 'Camry', 'color': 'Blue'}
```

---

**Q8. Write a program to check if a key exists in a dictionary. If it exists, print its value; if not, print "Key not found".**

✅ **Solution:**
```python
inventory = {'apples': 50, 'bananas': 30, 'mangoes': 20}

key = input("Enter item to search: ")

if key in inventory:
    print(f"{key} found! Quantity: {inventory[key]}")
else:
    print("Key not found")
```

**Sample Output:**
```
Enter item to search: bananas
bananas found! Quantity: 30
```

---

**Q9. Write a program to count the frequency of each character in a string using a dictionary.**

✅ **Solution:**
```python
text = "hello"
freq = {}

for char in text:
    freq[char] = freq.get(char, 0) + 1

print(freq)
```

**Output:**
```
{'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

💡 **Key Tip:** `.get(char, 0)` returns 0 if the character isn't in the dict yet — avoids `KeyError`.

---

**Q10. Merge two dictionaries into one.**

✅ **Solution:**
```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}

# Method 1: update()
merged = dict1.copy()
merged.update(dict2)
print("Merged:", merged)

# Method 2: ** unpacking (Python 3.5+)
merged2 = {**dict1, **dict2}
print("Merged2:", merged2)
```

**Output:**
```
Merged: {'a': 1, 'b': 2, 'c': 3, 'd': 4}
Merged2: {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program that takes a list of words and returns a dictionary with each word as a key and its length as the value.**

✅ **Solution:**
```python
words = ['python', 'java', 'javascript', 'c', 'ruby']

# Build dictionary using a loop
word_length = {}
for word in words:
    word_length[word] = len(word)

print(word_length)

# --- Alternative: Dictionary Comprehension ---
word_length2 = {word: len(word) for word in words}
print(word_length2)
```

**Output:**
```
{'python': 6, 'java': 4, 'javascript': 10, 'c': 1, 'ruby': 4}
```

---

**Q12. Write a program to find the student with the highest marks from a dictionary.**

✅ **Solution:**
```python
students = {
    'Alice': 88,
    'Bob': 95,
    'Charlie': 72,
    'Diana': 91
}

# Find the key with maximum value
topper = max(students, key=lambda x: students[x])

print(f"Topper: {topper} with {students[topper]} marks")
```

**Output:**
```
Topper: Bob with 95 marks
```

💡 **Step-by-step:**
1. `max()` iterates over keys
2. `key=lambda x: students[x]` tells max to compare by value
3. Returns the key (name) with the highest value (marks)

---

**Q13. Write a program to invert a dictionary — swap keys and values.**

✅ **Solution:**
```python
original = {'a': 1, 'b': 2, 'c': 3}

# Invert using dictionary comprehension
inverted = {value: key for key, value in original.items()}

print("Original:", original)
print("Inverted:", inverted)
```

**Output:**
```
Original: {'a': 1, 'b': 2, 'c': 3}
Inverted: {1: 'a', 2: 'b', 3: 'c'}
```

💡 **Note:** This only works cleanly if all values are unique. If values repeat, some keys will be lost in inversion.

---

**Q14. Write a program to group a list of names by their first letter using a dictionary.**

✅ **Solution:**
```python
names = ['Alice', 'Bob', 'Anna', 'Charlie', 'Brian', 'Catherine']

grouped = {}

for name in names:
    first = name[0]  # Get first letter
    if first not in grouped:
        grouped[first] = []  # Create empty list for new letter
    grouped[first].append(name)

for letter, group in grouped.items():
    print(f"{letter}: {group}")
```

**Output:**
```
A: ['Alice', 'Anna']
B: ['Bob', 'Brian']
C: ['Charlie', 'Catherine']
```

---

**Q15. Write a program to find common keys between two dictionaries and print their combined values.**

✅ **Solution:**
```python
dict1 = {'a': 10, 'b': 20, 'c': 30}
dict2 = {'b': 5,  'c': 15, 'd': 25}

# Find common keys
common_keys = dict1.keys() & dict2.keys()
print("Common Keys:", common_keys)

# Print combined (summed) values for common keys
print("\nCombined values for common keys:")
for key in common_keys:
    total = dict1[key] + dict2[key]
    print(f"  '{key}': {dict1[key]} + {dict2[key]} = {total}")
```

**Output:**
```
Common Keys: {'b', 'c'}

Combined values for common keys:
  'b': 20 + 5 = 25
  'c': 30 + 15 = 45
```

---

---

## 📘 Topic 2: Lists

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `l = []` | Create empty list |
| `l = [1, 2, 3]` | Create list with values |
| `l[0]` | Access by index |
| `l[-1]` | Last element |
| `l[1:3]` | Slicing |
| `l.append(x)` | Add to end |
| `l.insert(i, x)` | Insert at index i |
| `l.extend([x,y])` | Add multiple elements |
| `l.remove(x)` | Remove first occurrence of x |
| `l.pop(i)` | Remove & return element at index i |
| `l.sort()` | Sort in place |
| `l.reverse()` | Reverse in place |
| `len(l)` | Length of list |
| `x in l` | Check membership |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a List in Python? State its key properties.**

✅ **Answer:**
- A list is an **ordered, mutable** collection of elements.
- Elements can be of **any data type** (int, string, float, even another list).
- Lists are defined using **square brackets `[]`**.
- Lists allow **duplicate** values.
- Elements are accessed using **zero-based indexing**.

```python
my_list = [10, 'hello', 3.14, True]
print(my_list[1])  # hello
```

---

**Q2. What is the output?**

```python
l = [10, 20, 30, 40, 50]

print(l[1])
print(l[-1])
print(l[1:4])
print(l[:3])
print(l[::2])
```

✅ **Answer:**
```
20
50
[20, 30, 40]
[10, 20, 30]
[10, 30, 50]
```

💡 **Key Tip:** `l[::2]` means start to end, step 2 — picks every alternate element.

---

**Q3. True or False — with reason.**

```
a) Lists are immutable.
b) A list can contain another list as an element.
c) l.sort() returns a new sorted list.
d) l.append([1,2]) adds two elements to the list.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Lists are immutable | ❌ False | Lists are **mutable** — elements can be changed |
| b) List inside a list | ✅ True | This is called a **nested list** |
| c) `sort()` returns new list | ❌ False | `sort()` sorts **in-place** and returns `None` |
| d) `append([1,2])` adds 2 elements | ❌ False | It adds the **list as one element** — use `extend()` instead |

---

**Q4. Fill in the blank.**

```python
nums = [5, 3, 8, 1, 9, 2]

# Sort in ascending order
nums.______()
print(nums)

# Reverse the list
nums.______()
print(nums)

# Remove the value 8
nums.______(8)
print(nums)

# Add 100 at the end
nums.______(100)
print(nums)
```

✅ **Answer:**
```python
nums.sort()
nums.reverse()
nums.remove(8)
nums.append(100)
```

**Output:**
```
[1, 2, 3, 5, 8, 9]
[9, 8, 5, 3, 2, 1]
[9, 5, 3, 2, 1]
[9, 5, 3, 2, 1, 100]
```

---

**Q5. What is the output?**

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
print(b)

c = a.copy()
c.append(99)
print(a)
print(c)
```

✅ **Answer:**
```
[1, 2, 3, 4]
[1, 2, 3, 4]
[1, 2, 3, 4]
[1, 2, 3, 4, 99]
```

💡 **Key Tip:** `b = a` makes both point to the **same list** in memory. `a.copy()` creates an **independent copy**.

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a program to take 5 numbers from the user, store them in a list, and print the list.**

✅ **Solution:**
```python
numbers = []

for i in range(5):
    num = int(input(f"Enter number {i+1}: "))
    numbers.append(num)

print("Your list:", numbers)
```

**Sample Output:**
```
Enter number 1: 10
Enter number 2: 20
Enter number 3: 30
Enter number 4: 40
Enter number 5: 50
Your list: [10, 20, 30, 40, 50]
```

---

**Q7. Write a program to find the largest and smallest number in a list.**

✅ **Solution:**
```python
nums = [34, 7, 23, 32, 5, 62]

print("List:", nums)
print("Largest:", max(nums))
print("Smallest:", min(nums))
```

**Output:**
```
List: [34, 7, 23, 32, 5, 62]
Largest: 62
Smallest: 5
```

---

**Q8. Write a program to remove duplicate elements from a list.**

✅ **Solution:**
```python
nums = [1, 2, 2, 3, 4, 4, 5, 1]

unique = []
for num in nums:
    if num not in unique:
        unique.append(num)

print("Original:", nums)
print("Without duplicates:", unique)

# --- Alternative: using set ---
unique2 = list(set(nums))
print("Using set:", unique2)
```

**Output:**
```
Original: [1, 2, 2, 3, 4, 4, 5, 1]
Without duplicates: [1, 2, 3, 4, 5]
Using set: [1, 2, 3, 4, 5]
```

---

**Q9. Write a program to split a list into two halves.**

✅ **Solution:**
```python
l = [10, 20, 30, 40, 50, 60]

mid = len(l) // 2

first_half  = l[:mid]
second_half = l[mid:]

print("Original:   ", l)
print("First Half: ", first_half)
print("Second Half:", second_half)
```

**Output:**
```
Original:    [10, 20, 30, 40, 50, 60]
First Half:  [10, 20, 30]
Second Half: [40, 50, 60]
```

---

**Q10. Write a program to count how many times a specific element appears in a list.**

✅ **Solution:**
```python
items = ['apple', 'banana', 'apple', 'cherry', 'apple', 'banana']

search = input("Enter item to count: ")
count = items.count(search)

print(f"'{search}' appears {count} time(s) in the list.")
```

**Sample Output:**
```
Enter item to count: apple
'apple' appears 3 time(s) in the list.
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program to find all even and odd numbers from a list and store them in separate lists.**

✅ **Solution:**
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

evens = []
odds  = []

for num in numbers:
    if num % 2 == 0:
        evens.append(num)
    else:
        odds.append(num)

print("Original:", numbers)
print("Evens:   ", evens)
print("Odds:    ", odds)
```

**Output:**
```
Original: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Evens:    [2, 4, 6, 8, 10]
Odds:     [1, 3, 5, 7, 9]
```

---

**Q12. Write a program to flatten a nested list (list of lists) into a single list.**

✅ **Solution:**
```python
nested = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]

flat = []
for sublist in nested:
    for item in sublist:
        flat.append(item)

print("Nested:", nested)
print("Flat:  ", flat)
```

**Output:**
```
Nested: [[1, 2, 3], [4, 5], [6, 7, 8, 9]]
Flat:   [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

💡 **Step-by-step:**
1. Outer loop iterates over each **sublist**
2. Inner loop iterates over each **item** in the sublist
3. Each item is appended to `flat`

---

**Q13. Write a program to rotate a list by `n` positions to the left.**

✅ **Solution:**
```python
def rotate_left(lst, n):
    n = n % len(lst)        # Handle n > length
    return lst[n:] + lst[:n]

my_list = [1, 2, 3, 4, 5]
n = 2

rotated = rotate_left(my_list, n)
print(f"Original:      {my_list}")
print(f"Rotated by {n}: {rotated}")
```

**Output:**
```
Original:      [1, 2, 3, 4, 5]
Rotated by 2: [3, 4, 5, 1, 2]
```

💡 **Step-by-step:**
1. `lst[n:]` → takes from index 2 to end → `[3, 4, 5]`
2. `lst[:n]` → takes from start to index 2 → `[1, 2]`
3. Concatenating gives `[3, 4, 5, 1, 2]`

---

**Q14. Write a program to find the second largest number in a list without using `sort()`.**

✅ **Solution:**
```python
nums = [10, 45, 2, 78, 34, 56]

largest        = float('-inf')
second_largest = float('-inf')

for num in nums:
    if num > largest:
        second_largest = largest   # Old largest becomes 2nd
        largest = num
    elif num > second_largest and num != largest:
        second_largest = num

print("List:          ", nums)
print("Largest:       ", largest)
print("Second Largest:", second_largest)
```

**Output:**
```
List:           [10, 45, 2, 78, 34, 56]
Largest:        78
Second Largest: 56
```

---

**Q15. Write a program to merge two sorted lists into one sorted list without using `sort()`.**

✅ **Solution:**
```python
list1 = [1, 3, 5, 7]
list2 = [2, 4, 6, 8]

merged = []
i = 0
j = 0

# Compare elements from both lists
while i < len(list1) and j < len(list2):
    if list1[i] < list2[j]:
        merged.append(list1[i])
        i += 1
    else:
        merged.append(list2[j])
        j += 1

# Append remaining elements
merged.extend(list1[i:])
merged.extend(list2[j:])

print("List 1:", list1)
print("List 2:", list2)
print("Merged:", merged)
```

**Output:**
```
List 1: [1, 3, 5, 7]
List 2: [2, 4, 6, 8]
Merged: [1, 2, 3, 4, 5, 6, 7, 8]
```

---

---

## 📘 Topic 3: Tuples

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `t = ()` | Empty tuple |
| `t = (1, 2, 3)` | Create tuple |
| `t = (1,)` | Single element tuple (note the comma) |
| `t[0]` | Access by index |
| `t[-1]` | Last element |
| `t[1:3]` | Slicing |
| `len(t)` | Length |
| `t.count(x)` | Count occurrences of x |
| `t.index(x)` | Index of first x |
| `a, b, c = t` | Tuple unpacking |
| `t1 + t2` | Concatenate tuples |
| `x in t` | Membership check |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Tuple? How is it different from a List?**

✅ **Answer:**

| Feature | Tuple | List |
|---|---|---|
| Defined with | `()` | `[]` |
| Mutable | ❌ No | ✅ Yes |
| Ordered | ✅ Yes | ✅ Yes |
| Duplicates | ✅ Allowed | ✅ Allowed |
| Use case | Fixed data | Dynamic data |

```python
t = (1, 2, 3)
l = [1, 2, 3]

# This works:
l[0] = 99

# This raises TypeError:
# t[0] = 99
```

💡 **Key Tip:** Use tuples when data should not change (e.g., coordinates, RGB values, DB records).

---

**Q2. What is the output?**

```python
t = (10, 20, 30, 40, 50)

print(t[2])
print(t[-1])
print(t[1:4])
print(len(t))
print(t.count(20))
print(t.index(40))
```

✅ **Answer:**
```
30
50
(20, 30, 40)
5
1
3
```

---

**Q3. True or False — with reason.**

```
a) Tuples can be used as dictionary keys.
b) You can append to a tuple.
c) (5) is a tuple.
d) Tuple elements can be of mixed data types.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Tuples as dict keys | ✅ True | Tuples are **immutable**, so they're hashable |
| b) Append to tuple | ❌ False | Tuples are **immutable** — no append method |
| c) `(5)` is a tuple | ❌ False | `(5)` is just an **integer with parentheses** — use `(5,)` |
| d) Mixed data types | ✅ True | e.g., `(1, 'hello', 3.14)` is valid |

---

**Q4. Fill in the blank — Tuple Unpacking.**

```python
person = ('Alice', 25, 'Engineer')

# Unpack into variables
name, ______, profession = person

print(name)
print(age)
print(profession)
```

✅ **Answer:**
```python
name, age, profession = person
```

**Output:**
```
Alice
25
Engineer
```

---

**Q5. What is the output?**

```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

t3 = t1 + t2
print(t3)

t4 = t1 * 2
print(t4)

a, b, *rest = (10, 20, 30, 40, 50)
print(a)
print(b)
print(rest)
```

✅ **Answer:**
```
(1, 2, 3, 4, 5, 6)
(1, 2, 3, 1, 2, 3)
10
20
[30, 40, 50]
```

💡 **Key Tip:** `*rest` captures remaining elements as a **list**.

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Create a tuple of 5 fruits. Print each fruit using a loop.**

✅ **Solution:**
```python
fruits = ('apple', 'banana', 'cherry', 'mango', 'grape')

for fruit in fruits:
    print(fruit)
```

**Output:**
```
apple
banana
cherry
mango
grape
```

---

**Q7. Write a program to convert a list to a tuple and a tuple to a list.**

✅ **Solution:**
```python
my_list  = [1, 2, 3, 4, 5]
my_tuple = (10, 20, 30, 40, 50)

# List → Tuple
converted_tuple = tuple(my_list)
print("List to Tuple:", converted_tuple)
print("Type:", type(converted_tuple))

# Tuple → List
converted_list = list(my_tuple)
print("Tuple to List:", converted_list)
print("Type:", type(converted_list))
```

**Output:**
```
List to Tuple: (1, 2, 3, 4, 5)
Type: <class 'tuple'>
Tuple to List: [10, 20, 30, 40, 50]
Type: <class 'list'>
```

---

**Q8. Write a program to find the maximum and minimum values from a tuple.**

✅ **Solution:**
```python
scores = (88, 72, 95, 61, 84, 90)

print("Scores:", scores)
print("Max Score:", max(scores))
print("Min Score:", min(scores))
print("Sum of Scores:", sum(scores))
```

**Output:**
```
Scores: (88, 72, 95, 61, 84, 90)
Max Score: 95
Min Score: 61
Sum of Scores: 490
```

---

**Q9. Write a program to count the occurrences of an element in a tuple.**

✅ **Solution:**
```python
colors = ('red', 'blue', 'red', 'green', 'red', 'blue')

search = input("Enter color to count: ")
count = colors.count(search)

print(f"'{search}' appears {count} time(s).")
```

**Sample Output:**
```
Enter color to count: red
'red' appears 3 time(s).
```

---

**Q10. Write a program to swap two variables using tuple unpacking.**

✅ **Solution:**
```python
a = 10
b = 20

print(f"Before: a = {a}, b = {b}")

# Swap using tuple unpacking
a, b = b, a

print(f"After:  a = {a}, b = {b}")
```

**Output:**
```
Before: a = 10, b = 20
After:  a = 20, b = 10
```

💡 **Key Tip:** Python packs `b, a` into a tuple on the right, then unpacks into `a, b` on the left — clean and Pythonic!

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program to find the index of the largest element in a tuple.**

✅ **Solution:**
```python
nums = (34, 89, 12, 56, 78, 90, 45)

largest = max(nums)
index   = nums.index(largest)

print("Tuple:  ", nums)
print("Largest:", largest)
print("Index:  ", index)
```

**Output:**
```
Tuple:   (34, 89, 12, 56, 78, 90, 45)
Largest: 90
Index:   5
```

---

**Q12. Write a program to zip two tuples together and display the result as a list of tuples.**

✅ **Solution:**
```python
names  = ('Alice', 'Bob', 'Charlie')
scores = (88, 92, 75)

# Zip the two tuples
combined = list(zip(names, scores))
print("Zipped:", combined)

# Display neatly
print("\nName - Score:")
for name, score in combined:
    print(f"  {name}: {score}")
```

**Output:**
```
Zipped: [('Alice', 88), ('Bob', 92), ('Charlie', 75)]

Name - Score:
  Alice: 88
  Bob: 92
  Charlie: 75
```

---

**Q13. Write a function that takes a tuple and returns a new tuple with duplicate elements removed.**

✅ **Solution:**
```python
def remove_duplicates(t):
    seen   = []
    result = []
    for item in t:
        if item not in seen:
            seen.append(item)
            result.append(item)
    return tuple(result)

# Test
original = (1, 2, 2, 3, 4, 4, 5, 1)
cleaned  = remove_duplicates(original)

print("Original:", original)
print("Cleaned: ", cleaned)
```

**Output:**
```
Original: (1, 2, 2, 3, 4, 4, 5, 1)
Cleaned:  (1, 2, 3, 4, 5)
```

---

**Q14. Write a program to sort a list of tuples by the second element (score).**

✅ **Solution:**
```python
students = [('Alice', 88), ('Bob', 92), ('Charlie', 75), ('Diana', 95)]

# Sort by second element (score) in descending order
sorted_students = sorted(students, key=lambda x: x[1], reverse=True)

print("Sorted by Score (Descending):")
for name, score in sorted_students:
    print(f"  {name}: {score}")
```

**Output:**
```
Sorted by Score (Descending):
  Diana: 95
  Bob: 92
  Alice: 88
  Charlie: 75
```

💡 **Step-by-step:**
1. `sorted()` returns a new sorted list
2. `key=lambda x: x[1]` sorts by the **second element** of each tuple
3. `reverse=True` gives **descending** order

---

**Q15. Write a program to unpack a nested tuple and print each element.**

✅ **Solution:**
```python
nested = ((1, 2), (3, 4), (5, 6))

print("Nested Tuple:", nested)
print("\nUnpacked:")

for pair in nested:
    a, b = pair
    print(f"  a = {a}, b = {b}, sum = {a + b}")

# Total sum
total = sum(a + b for a, b in nested)
print(f"\nTotal Sum: {total}")
```

**Output:**
```
Nested Tuple: ((1, 2), (3, 4), (5, 6))

Unpacked:
  a = 1, b = 2, sum = 3
  a = 3, b = 4, sum = 7
  a = 5, b = 6, sum = 11

Total Sum: 21
```

---

---

## 📘 Topic 4: Sets

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `s = set()` | Create empty set |
| `s = {1, 2, 3}` | Create set with values |
| `s.add(x)` | Add element |
| `s.remove(x)` | Remove element (raises error if missing) |
| `s.discard(x)` | Remove element (no error if missing) |
| `s.pop()` | Remove and return an arbitrary element |
| `s1 \| s2` | Union |
| `s1 & s2` | Intersection |
| `s1 - s2` | Difference |
| `s1 ^ s2` | Symmetric difference |
| `s1.issubset(s2)` | Check if s1 ⊆ s2 |
| `s1.issuperset(s2)` | Check if s1 ⊇ s2 |
| `len(s)` | Number of elements |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Set in Python? State its key properties.**

✅ **Answer:**
- A set is an **unordered, mutable** collection of **unique** elements.
- Defined using `{}` or `set()`.
- **No duplicate values** allowed — duplicates are automatically removed.
- **No indexing** — you cannot access elements by position.
- Supports mathematical **set operations**: union, intersection, difference.

```python
s = {1, 2, 3, 2, 1}
print(s)  # {1, 2, 3} — duplicates removed
```

---

**Q2. What is the output?**

```python
s1 = {1, 2, 3, 4, 5}
s2 = {4, 5, 6, 7, 8}

print(s1 | s2)   # Union
print(s1 & s2)   # Intersection
print(s1 - s2)   # Difference
print(s1 ^ s2)   # Symmetric Difference
```

✅ **Answer:**
```
{1, 2, 3, 4, 5, 6, 7, 8}
{4, 5}
{1, 2, 3}
{1, 2, 3, 6, 7, 8}
```

💡 **Key Tip:** Symmetric difference (`^`) = elements in **either** set but **not both**.

---

**Q3. True or False — with reason.**

```
a) Sets maintain insertion order.
b) {1, 2, 2, 3} creates a set with 4 elements.
c) You can access set elements using index like s[0].
d) An empty set must be created with set(), not {}.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Sets maintain order | ❌ False | Sets are **unordered** |
| b) `{1,2,2,3}` has 4 elements | ❌ False | Duplicates removed → **3 elements** |
| c) `s[0]` works | ❌ False | Sets do **not support indexing** |
| d) Empty set = `set()` | ✅ True | `{}` creates an empty **dict**, not a set |

---

**Q4. Fill in the blank.**

```python
fruits = {'apple', 'banana', 'cherry'}

# Add 'mango'
fruits.______(______)

# Remove 'banana'
fruits.______(______)

# Check if 'apple' is in the set
print(______ in fruits)

# Print the number of elements
print(______(fruits))
```

✅ **Answer:**
```python
fruits.add('mango')
fruits.remove('banana')
print('apple' in fruits)
print(len(fruits))
```

**Output:**
```
True
3
```

---

**Q5. What is the output?**

```python
s = {5, 3, 1, 4, 2}
print(s)

s.add(3)
print(s)

s.discard(10)   # No error
print(s)

print(sorted(s))
```

✅ **Answer:**
```
{1, 2, 3, 4, 5}   # Order may vary
{1, 2, 3, 4, 5}   # 3 already exists, not added again
{1, 2, 3, 4, 5}   # 10 not present, discard does nothing
[1, 2, 3, 4, 5]   # sorted() returns a sorted list
```

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a program to remove all duplicate values from a list using a set.**

✅ **Solution:**
```python
nums = [1, 2, 2, 3, 4, 4, 5, 1, 6]

unique = list(set(nums))

print("Original:", nums)
print("Unique:  ", unique)
```

**Output:**
```
Original: [1, 2, 2, 3, 4, 4, 5, 1, 6]
Unique:   [1, 2, 3, 4, 5, 6]
```

---

**Q7. Write a program to find union and intersection of two sets.**

✅ **Solution:**
```python
set_a = {1, 2, 3, 4, 5}
set_b = {3, 4, 5, 6, 7}

union        = set_a | set_b
intersection = set_a & set_b

print("Set A:       ", set_a)
print("Set B:       ", set_b)
print("Union:       ", union)
print("Intersection:", intersection)
```

**Output:**
```
Set A:        {1, 2, 3, 4, 5}
Set B:        {3, 4, 5, 6, 7}
Union:        {1, 2, 3, 4, 5, 6, 7}
Intersection: {3, 4, 5}
```

---

**Q8. Write a program to check if one set is a subset of another.**

✅ **Solution:**
```python
all_students     = {'Alice', 'Bob', 'Charlie', 'Diana', 'Eve'}
present_students = {'Alice', 'Charlie', 'Eve'}

if present_students.issubset(all_students):
    print("All present students are valid students.")
else:
    print("Some students are not in the system.")

absent = all_students - present_students
print("Absent students:", absent)
```

**Output:**
```
All present students are valid students.
Absent students: {'Bob', 'Diana'}
```

---

**Q9. Write a program to find elements that are in one set but not in another (difference).**

✅ **Solution:**
```python
skills_alice = {'Python', 'Java', 'SQL', 'Linux'}
skills_bob   = {'Java', 'C++', 'SQL', 'JavaScript'}

only_alice = skills_alice - skills_bob
only_bob   = skills_bob - skills_alice
common     = skills_alice & skills_bob

print("Only Alice knows:", only_alice)
print("Only Bob knows:  ", only_bob)
print("Both know:       ", common)
```

**Output:**
```
Only Alice knows: {'Python', 'Linux'}
Only Bob knows:   {'C++', 'JavaScript'}
Both know:        {'Java', 'SQL'}
```

---

**Q10. Write a program to add and discard elements from a set safely.**

✅ **Solution:**
```python
s = {10, 20, 30}

# Add elements
s.add(40)
s.add(20)     # Already exists — no change

# Discard safely (no error if missing)
s.discard(30)
s.discard(99) # 99 not in set — no error

print("Final Set:", s)
print("Size:", len(s))
```

**Output:**
```
Final Set: {10, 20, 40}
Size: 3
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program that takes two lists, converts them to sets, and finds all four set operations.**

✅ **Solution:**
```python
list1 = [1, 2, 3, 4, 5, 3, 2]
list2 = [3, 4, 5, 6, 7, 4, 5]

s1 = set(list1)
s2 = set(list2)

print("Set 1:", s1)
print("Set 2:", s2)
print()
print("Union (|):                 ", s1 | s2)
print("Intersection (&):          ", s1 & s2)
print("Difference s1-s2 (-):      ", s1 - s2)
print("Symmetric Difference (^):  ", s1 ^ s2)
```

**Output:**
```
Set 1: {1, 2, 3, 4, 5}
Set 2: {3, 4, 5, 6, 7}

Union (|):                  {1, 2, 3, 4, 5, 6, 7}
Intersection (&):           {3, 4, 5}
Difference s1-s2 (-):       {1, 2}
Symmetric Difference (^):   {1, 2, 6, 7}
```

---

**Q12. Write a program to find common elements between three sets.**

✅ **Solution:**
```python
batch_a = {'Alice', 'Bob', 'Charlie', 'Diana'}
batch_b = {'Bob', 'Charlie', 'Eve', 'Frank'}
batch_c = {'Charlie', 'Bob', 'Grace', 'Alice'}

# Common in all three
common_all = batch_a & batch_b & batch_c

# Common in at least two
common_ab = batch_a & batch_b
common_bc = batch_b & batch_c
common_ac = batch_a & batch_c

print("Common in ALL three:    ", common_all)
print("Common in A & B:        ", common_ab)
print("Common in B & C:        ", common_bc)
print("Common in A & C:        ", common_ac)
```

**Output:**
```
Common in ALL three:     {'Charlie', 'Bob'}
Common in A & B:         {'Bob', 'Charlie'}
Common in B & C:         {'Bob', 'Charlie'}
Common in A & C:         {'Alice', 'Charlie', 'Bob'}
```

---

**Q13. Write a program to find all unique characters in a string using a set.**

✅ **Solution:**
```python
text = input("Enter a string: ")

unique_chars = set(text.replace(" ", ""))  # Exclude spaces

print(f"\nOriginal String: {text}")
print(f"Unique Characters: {unique_chars}")
print(f"Total Unique Characters: {len(unique_chars)}")

# Sorted display
print(f"Sorted Unique: {sorted(unique_chars)}")
```

**Sample Output:**
```
Enter a string: hello world

Original String: hello world
Unique Characters: {'h', 'e', 'l', 'o', 'w', 'r', 'd'}
Total Unique Characters: 7
Sorted Unique: ['d', 'e', 'h', 'l', 'o', 'r', 'w']
```

---

**Q14. Write a program to check if two sets are disjoint (no common elements).**

✅ **Solution:**
```python
def check_disjoint(s1, s2):
    if s1.isdisjoint(s2):
        print("Sets are DISJOINT — no common elements.")
    else:
        common = s1 & s2
        print(f"Sets are NOT disjoint — Common elements: {common}")

set1 = {1, 2, 3}
set2 = {4, 5, 6}
set3 = {3, 6, 9}

check_disjoint(set1, set2)
check_disjoint(set1, set3)
```

**Output:**
```
Sets are DISJOINT — no common elements.
Sets are NOT disjoint — Common elements: {3}
```

---

**Q15. Write a program that reads a sentence, and prints all unique words and duplicate words.**

✅ **Solution:**
```python
sentence = input("Enter a sentence: ")
words    = sentence.lower().split()

seen       = set()
duplicates = set()

for word in words:
    if word in seen:
        duplicates.add(word)
    else:
        seen.add(word)

unique_only = seen - duplicates

print(f"\nAll unique words (first occurrence only): {seen}")
print(f"Words that appear MORE than once:         {duplicates}")
print(f"Words that appear EXACTLY once:           {unique_only}")
```

**Sample Output:**
```
Enter a sentence: the cat sat on the mat and the cat

All unique words (first occurrence only): {'the', 'cat', 'sat', 'on', 'mat', 'and'}
Words that appear MORE than once:         {'the', 'cat'}
Words that appear EXACTLY once:           {'sat', 'on', 'mat', 'and'}
```

---

---

## 📘 Topic 5: Strings

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `s = "hello"` | Create string |
| `s[0]` | Access character |
| `s[-1]` | Last character |
| `s[1:4]` | Slicing |
| `s.upper()` | Convert to uppercase |
| `s.lower()` | Convert to lowercase |
| `s.strip()` | Remove leading/trailing whitespace |
| `s.split(x)` | Split by delimiter x |
| `s.replace(a, b)` | Replace a with b |
| `s.find(x)` | Index of first x (-1 if not found) |
| `s.count(x)` | Count occurrences of x |
| `s.startswith(x)` | Starts with x? |
| `s.endswith(x)` | Ends with x? |
| `'sep'.join(list)` | Join list into string |
| `f"Hello {name}"` | f-string formatting |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What are strings in Python? State any 4 properties.**

✅ **Answer:**
- Strings are **ordered sequences of characters** enclosed in `' '` or `" "`.
- Strings are **immutable** — characters cannot be changed after creation.
- Strings support **indexing and slicing** like lists.
- Strings support **concatenation** (`+`) and **repetition** (`*`).
- Strings are **iterable** — you can loop over each character.

```python
s = "Python"
print(s[0])    # P
print(s[-1])   # n
print(s[0:3])  # Pyt
print(s * 2)   # PythonPython
```

---

**Q2. What is the output?**

```python
s = "  Hello, Python World!  "

print(s.strip())
print(s.upper())
print(s.lower())
print(s.replace("Python", "Beautiful"))
print(s.count('l'))
print(s.find('Python'))
```

✅ **Answer:**
```
Hello, Python World!
  HELLO, PYTHON WORLD!  
  hello, python world!  
  Hello, Beautiful World!  
3
9
```

---

**Q3. True or False — with reason.**

```
a) Strings are mutable in Python.
b) "hello"[1:4] returns "ell".
c) "hello" + 5 is valid.
d) f-strings are the preferred way to format strings in modern Python.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Strings are mutable | ❌ False | Strings are **immutable** in Python |
| b) `"hello"[1:4]` = "ell" | ✅ True | Index 1,2,3 → `e`, `l`, `l` |
| c) `"hello" + 5` is valid | ❌ False | Can't concatenate `str` and `int` — use `str(5)` |
| d) f-strings are preferred | ✅ True | Introduced in Python 3.6, readable and fast |

---

**Q4. Fill in the blank.**

```python
s = "python programming"

# Capitalize first letter
print(s.______())

# Check if string starts with 'python'
print(s.______('python'))

# Split into a list of words
words = s.______()
print(words)

# Join words back with '-'
joined = '______'.join(words)
print(joined)
```

✅ **Answer:**
```python
print(s.capitalize())
print(s.startswith('python'))
words = s.split()
joined = '-'.join(words)
```

**Output:**
```
Python programming
True
['python', 'programming']
python-programming
```

---

**Q5. What is the output?**

```python
s = "abcdef"

print(s[::-1])
print(s[::2])
print(s[1::2])

name = "Alice"
age  = 25
print(f"My name is {name} and I am {age} years old.")
```

✅ **Answer:**
```
fedcba
ace
bdf
My name is Alice and I am 25 years old.
```

💡 **Key Tip:** `s[::-1]` reverses a string — `step = -1` means go backwards.

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a program to check if a string is a palindrome.**

✅ **Solution:**
```python
word = input("Enter a word: ")

cleaned  = word.lower().replace(" ", "")
reversed_word = cleaned[::-1]

if cleaned == reversed_word:
    print(f"'{word}' is a PALINDROME ✅")
else:
    print(f"'{word}' is NOT a palindrome ❌")
```

**Sample Output:**
```
Enter a word: Racecar
'Racecar' is a PALINDROME ✅
```

---

**Q7. Write a program to count the number of vowels and consonants in a string.**

✅ **Solution:**
```python
text   = input("Enter a string: ").lower()
vowels = "aeiou"

vowel_count     = 0
consonant_count = 0

for char in text:
    if char.isalpha():
        if char in vowels:
            vowel_count += 1
        else:
            consonant_count += 1

print(f"Vowels:     {vowel_count}")
print(f"Consonants: {consonant_count}")
```

**Sample Output:**
```
Enter a string: Hello World
Vowels:     3
Consonants: 7
```

---

**Q8. Write a program to reverse the words in a sentence.**

✅ **Solution:**
```python
sentence = input("Enter a sentence: ")

words         = sentence.split()
reversed_words = words[::-1]
result        = ' '.join(reversed_words)

print("Original: ", sentence)
print("Reversed: ", result)
```

**Sample Output:**
```
Enter a sentence: Python is fun
Original:  Python is fun
Reversed:  fun is Python
```

---

**Q9. Write a program to replace all spaces in a string with underscores.**

✅ **Solution:**
```python
text = input("Enter a sentence: ")

result = text.replace(' ', '_')

print("Original:  ", text)
print("Converted: ", result)
```

**Sample Output:**
```
Enter a sentence: Hello World How Are You
Original:   Hello World How Are You
Converted:  Hello_World_How_Are_You
```

---

**Q10. Write a program to count the frequency of each word in a sentence.**

✅ **Solution:**
```python
sentence = input("Enter a sentence: ").lower()
words    = sentence.split()

freq = {}
for word in words:
    freq[word] = freq.get(word, 0) + 1

print("\nWord Frequencies:")
for word, count in freq.items():
    print(f"  {word}: {count}")
```

**Sample Output:**
```
Enter a sentence: the cat sat on the mat and the cat

Word Frequencies:
  the: 3
  cat: 2
  sat: 1
  on: 1
  mat: 1
  and: 1
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program to check if two strings are anagrams of each other.**

✅ **Solution:**
```python
def are_anagrams(s1, s2):
    # Remove spaces and convert to lowercase
    s1 = s1.lower().replace(" ", "")
    s2 = s2.lower().replace(" ", "")

    # Compare sorted characters
    return sorted(s1) == sorted(s2)

word1 = input("Enter first word:  ")
word2 = input("Enter second word: ")

if are_anagrams(word1, word2):
    print(f"'{word1}' and '{word2}' ARE anagrams ✅")
else:
    print(f"'{word1}' and '{word2}' are NOT anagrams ❌")
```

**Sample Output:**
```
Enter first word:  listen
Enter second word: silent
'listen' and 'silent' ARE anagrams ✅
```

---

**Q12. Write a program to find the most frequently occurring character in a string.**

✅ **Solution:**
```python
text = input("Enter a string: ").lower().replace(" ", "")

# Build frequency dictionary
freq = {}
for char in text:
    freq[char] = freq.get(char, 0) + 1

# Find max
max_char  = max(freq, key=lambda x: freq[x])
max_count = freq[max_char]

print(f"\nCharacter Frequencies: {freq}")
print(f"Most Frequent: '{max_char}' → {max_count} times")
```

**Sample Output:**
```
Enter a string: programming
Character Frequencies: {'p': 1, 'r': 2, 'o': 1, 'g': 2, 'a': 1, 'm': 2, 'i': 1, 'n': 1}
Most Frequent: 'r' → 2 times
```

---

**Q13. Write a program to check if a string contains only alphanumeric characters (no symbols or spaces).**

✅ **Solution:**
```python
def is_alphanumeric(s):
    for char in s:
        if not (char.isalpha() or char.isdigit()):
            return False
    return True

test_strings = ["Hello123", "Hello World", "Python3!", "abc456"]

for s in test_strings:
    result = "✅ Alphanumeric" if is_alphanumeric(s) else "❌ Not Alphanumeric"
    print(f"  '{s}' → {result}")
```

**Output:**
```
  'Hello123' → ✅ Alphanumeric
  'Hello World' → ❌ Not Alphanumeric
  'Python3!' → ❌ Not Alphanumeric
  'abc456' → ✅ Alphanumeric
```

---

**Q14. Write a program to truncate a string to a given number of characters and add "..." if truncated.**

✅ **Solution:**
```python
def truncate(text, limit):
    if len(text) <= limit:
        return text
    else:
        return text[:limit] + "..."

sentences = [
    "Hi",
    "Python is great",
    "This is a very long sentence that should be truncated"
]

limit = 15
print(f"Limit: {limit} characters\n")

for s in sentences:
    print(f"  Original:  '{s}'")
    print(f"  Truncated: '{truncate(s, limit)}'")
    print()
```

**Output:**
```
Limit: 15 characters

  Original:  'Hi'
  Truncated: 'Hi'

  Original:  'Python is great'
  Truncated: 'Python is great'

  Original:  'This is a very long sentence that should be truncated'
  Truncated: 'This is a very...'
```

---

**Q15. Write a program to title-case a sentence (capitalize the first letter of each word) without using `.title()`.**

✅ **Solution:**
```python
def manual_title_case(sentence):
    words  = sentence.split()
    result = []

    for word in words:
        # Capitalize first letter, keep rest lowercase
        titled = word[0].upper() + word[1:].lower()
        result.append(titled)

    return ' '.join(result)

sentences = [
    "hello world",
    "python is awesome",
    "the quick BROWN fox"
]

for s in sentences:
    print(f"  Input:  '{s}'")
    print(f"  Output: '{manual_title_case(s)}'")
    print()
```

**Output:**
```
  Input:  'hello world'
  Output: 'Hello World'

  Input:  'python is awesome'
  Output: 'Python Is Awesome'

  Input:  'the quick BROWN fox'
  Output: 'The Quick Brown Fox'
```

---

---

## 📊 Part 1 Summary

| Topic | Q1–Q5 | Q6–Q10 | Q11–Q15 | Total |
|---|---|---|---|---|
| 📘 Dictionaries | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 📘 Lists | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 📘 Tuples | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 📘 Sets | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 📘 Strings | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| | | | **TOTAL** | **75 Questions** |

---

> 💡 **Exam Tip:** Focus on understanding the **mutability rules**:
> `List ✅ mutable` | `Tuple ❌ immutable` | `Set ✅ mutable but unordered` | `Dict ✅ mutable` | `String ❌ immutable`

---

*📁 Part of: Python-Exam-Prep Series | PGCP-ITISS | February 2026*
*➡️ Next: [Part 2 — Functions, Lambda/Map/Filter, Regular Expressions](Part2_Functions.md)*