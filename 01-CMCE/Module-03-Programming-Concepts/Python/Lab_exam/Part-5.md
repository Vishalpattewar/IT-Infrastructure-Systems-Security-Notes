# 🐍 Python — Part 5: Exam Focus

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Sections](https://img.shields.io/badge/Sections-5-green)
![Programs](https://img.shields.io/badge/Programs-38-orange)
![Level](https://img.shields.io/badge/Level-Basic%20to%20Medium-yellow)

---

## 📌 Index

| # | Section | Programs |
|---|---|---|
| 1 | [📘 Lists](#-section-1-lists) | P1–P8 |
| 2 | [📘 Dictionaries](#-section-2-dictionaries) | P1–P8 |
| 3 | [⚙️ Functions](#️-section-3-functions) | P1–P8 |
| 4 | [🏛️ Classes & Objects](#️-section-4-classes--objects) | P1–P8 |
| 5 | [🌐 Sockets](#-section-5-sockets) | P1–P6 |

---

---

## 📘 Section 1: Lists

---

### 🟢 P1. Store and Display Roll Numbers of Students

**📝 Problem:**
Take roll numbers of 5 students as input, store them in a list, and display all roll numbers.

✅ **Solution:**

```python
roll_numbers = []

print("Enter roll numbers of 5 students:")
for i in range(5):
    roll = int(input(f"  Student {i + 1} Roll No: "))
    roll_numbers.append(roll)

print("\nAll Roll Numbers:")
for i, roll in enumerate(roll_numbers, 1):
    print(f"  Student {i}: {roll}")

print(f"\nTotal Students: {len(roll_numbers)}")
```

**Output:**
```
Enter roll numbers of 5 students:
  Student 1 Roll No: 101
  Student 2 Roll No: 102
  Student 3 Roll No: 103
  Student 4 Roll No: 104
  Student 5 Roll No: 105

All Roll Numbers:
  Student 1: 101
  Student 2: 102
  Student 3: 103
  Student 4: 104
  Student 5: 105

Total Students: 5
```

💡 `enumerate(list, 1)` gives index starting from 1 instead of 0.

---

### 🟢 P2. Sum and Average of a List of Numbers

**📝 Problem:**
Take n numbers from the user, store in a list, and display the sum and average.

✅ **Solution:**

```python
numbers = []

n = int(input("How many numbers do you want to enter? "))

for i in range(n):
    num = float(input(f"  Enter number {i + 1}: "))
    numbers.append(num)

# Calculate sum manually
total = 0
for num in numbers:
    total += num

# Calculate average
average = total / len(numbers)

print(f"\nNumbers : {numbers}")
print(f"Sum     : {total}")
print(f"Average : {average:.2f}")
```

**Output:**
```
How many numbers do you want to enter? 5
  Enter number 1: 10
  Enter number 2: 20
  Enter number 3: 30
  Enter number 4: 40
  Enter number 5: 50

Numbers : [10.0, 20.0, 30.0, 40.0, 50.0]
Sum     : 150.0
Average : 30.00
```

---

### 🟢 P3. Search for an Element in a List

**📝 Problem:**
Create a list of items. Take a search input from the user and check if it exists in the list. If found, display its position.

✅ **Solution:**

```python
items = ["apple", "banana", "cherry", "mango", "grape"]

print("Available items:", items)

search = input("\nEnter item to search: ")

# Search manually using loop
found    = False
position = -1

for i in range(len(items)):
    if items[i].lower() == search.lower():
        found    = True
        position = i + 1    # 1-based position
        break

if found:
    print(f"'{search}' found at position {position} ✅")
else:
    print(f"'{search}' not found in the list ❌")
```

**Output:**
```
Available items: ['apple', 'banana', 'cherry', 'mango', 'grape']

Enter item to search: mango
'mango' found at position 4 ✅

Enter item to search: orange
'orange' not found in the list ❌
```

💡 `.lower()` on both sides makes the search **case-insensitive**.

---

### 🟢 P4. Copy a List and Modify Without Affecting Original

**📝 Problem:**
Create a list of numbers. Make a copy of it, modify the copy, and show that the original remains unchanged.

✅ **Solution:**

```python
original = [10, 20, 30, 40, 50]

# Correct way to copy — using .copy()
copy = original.copy()

# Modify the copy
copy.append(60)
copy[0] = 99

print("Original List:", original)
print("Modified Copy:", copy)

# Wrong way demo
wrong_copy = original       # This is NOT a copy — both point to same list
wrong_copy.append(999)

print("\nAfter wrong copy modification:")
print("Original     :", original)     # Original is also changed!
print("Wrong Copy   :", wrong_copy)
```

**Output:**
```
Original List: [10, 20, 30, 40, 50]
Modified Copy: [99, 20, 30, 40, 50, 60]

After wrong copy modification:
Original     : [10, 20, 30, 40, 50, 999]
Wrong Copy   : [10, 20, 30, 40, 50, 999]
```

💡 Always use `.copy()` to make an independent copy. `b = a` just creates another reference to the **same list**.

---

### 🟡 P5. Student Attendance Tracker

**📝 Problem:**
Store student names in a list. Take attendance — mark each student present (P) or absent (A). Display a final attendance report.

✅ **Solution:**

```python
students   = ["Alice", "Bob", "Charlie", "Diana", "Eve"]
attendance = {}

print("── Mark Attendance ──────────────────")
for student in students:
    status = input(f"  {student} (P/A): ").strip().upper()
    while status not in ["P", "A"]:
        status = input(f"  Invalid. Enter P or A for {student}: ").strip().upper()
    attendance[student] = status

print("\n── Attendance Report ────────────────")
print(f"  {'Student':<12} {'Status'}")
print("  " + "-" * 22)

present_count = 0
absent_count  = 0

for student in students:
    status = attendance[student]
    label  = "Present ✅" if status == "P" else "Absent  ❌"
    print(f"  {student:<12} {label}")
    if status == "P":
        present_count += 1
    else:
        absent_count  += 1

print("  " + "-" * 22)
print(f"  Present: {present_count} | Absent: {absent_count}")
```

**Output:**
```
── Mark Attendance ──────────────────
  Alice (P/A): P
  Bob (P/A): A
  Charlie (P/A): P
  Diana (P/A): P
  Eve (P/A): A

── Attendance Report ────────────────
  Student      Status
  ----------------------
  Alice        Present ✅
  Bob          Absent  ❌
  Charlie      Present ✅
  Diana        Present ✅
  Eve          Absent  ❌
  ----------------------
  Present: 3 | Absent: 2
```

---

### 🟡 P6. Find Second Largest Number in a List

**📝 Problem:**
Take a list of numbers and find the second largest number without using sort().

✅ **Solution:**

```python
numbers = []

n = int(input("How many numbers? "))
for i in range(n):
    num = int(input(f"  Enter number {i + 1}: "))
    numbers.append(num)

# Find largest first
largest = numbers[0]
for num in numbers:
    if num > largest:
        largest = num

# Find second largest
second_largest = None
for num in numbers:
    if num == largest:
        continue
    if second_largest is None or num > second_largest:
        second_largest = num

print(f"\nNumbers        : {numbers}")
print(f"Largest        : {largest}")

if second_largest is not None:
    print(f"Second Largest : {second_largest}")
else:
    print("Second largest does not exist (all elements are equal).")
```

**Output:**
```
How many numbers? 6
  Enter number 1: 45
  Enter number 2: 12
  Enter number 3: 78
  Enter number 4: 34
  Enter number 5: 90
  Enter number 6: 56

Numbers        : [45, 12, 78, 34, 90, 56]
Largest        : 90
Second Largest : 78
```

💡 We skip the largest value and find the next highest using a separate loop pass.

---

### 🟡 P7. Separate Positive, Negative, and Zero

**📝 Problem:**
Take a list of numbers from the user and separate them into three lists — positive, negative, and zero.

✅ **Solution:**

```python
numbers = []

n = int(input("How many numbers? "))
for i in range(n):
    num = float(input(f"  Enter number {i + 1}: "))
    numbers.append(num)

positives = []
negatives = []
zeros     = []

for num in numbers:
    if num > 0:
        positives.append(num)
    elif num < 0:
        negatives.append(num)
    else:
        zeros.append(num)

print(f"\nAll Numbers : {numbers}")
print(f"Positives   : {positives}")
print(f"Negatives   : {negatives}")
print(f"Zeros       : {zeros}")
```

**Output:**
```
How many numbers? 7
  Enter number 1: 5
  Enter number 2: -3
  Enter number 3: 0
  Enter number 4: 8
  Enter number 5: -1
  Enter number 6: 0
  Enter number 7: 4

All Numbers : [5.0, -3.0, 0.0, 8.0, -1.0, 0.0, 4.0]
Positives   : [5.0, 8.0, 4.0]
Negatives   : [-3.0, -1.0]
Zeros       : [0.0, 0.0]
```

---

### 🟡 P8. Multiplication Table as a List

**📝 Problem:**
Take a number from the user and generate its multiplication table up to 10. Store results in a list and display.

✅ **Solution:**

```python
num = int(input("Enter a number for multiplication table: "))

table = []

for i in range(1, 11):
    result = num * i
    table.append(result)

print(f"\nMultiplication Table of {num}:")
print("-" * 25)

for i in range(len(table)):
    print(f"  {num} x {i + 1:2} = {table[i]}")

print(f"\nTable as list: {table}")
```

**Output:**
```
Enter a number for multiplication table: 5

Multiplication Table of 5:
-------------------------
  5 x  1 = 5
  5 x  2 = 10
  5 x  3 = 15
  5 x  4 = 20
  5 x  5 = 25
  5 x  6 = 30
  5 x  7 = 35
  5 x  8 = 40
  5 x  9 = 45
  5 x 10 = 50

Table as list: [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
```

---

---

## 📘 Section 2: Dictionaries

---

### 🟢 P1. Capital Cities of Countries

**📝 Problem:**
Create a dictionary of countries and their capital cities. Allow the user to search for a country and display its capital.

✅ **Solution:**

```python
capitals = {
    "India"          : "New Delhi",
    "USA"            : "Washington D.C.",
    "UK"             : "London",
    "France"         : "Paris",
    "Japan"          : "Tokyo",
    "Australia"      : "Canberra",
    "Germany"        : "Berlin",
}

print("Available Countries:", list(capitals.keys()))

country = input("\nEnter country name: ").strip()

if country in capitals:
    print(f"Capital of {country} is: {capitals[country]}")
else:
    print(f"'{country}' not found in the records.")
```

**Output:**
```
Available Countries: ['India', 'USA', 'UK', 'France', 'Japan', 'Australia', 'Germany']

Enter country name: France
Capital of France is: Paris

Enter country name: Canada
'Canada' not found in the records.
```

---

### 🟢 P2. Phone Book

**📝 Problem:**
Create a phone book using a dictionary. Perform: Add contact, Search contact, Display all contacts.

✅ **Solution:**

```python
phonebook = {}

def add_contact(name, number):
    phonebook[name] = number
    print(f"  ✅ '{name}' added.")

def search_contact(name):
    if name in phonebook:
        print(f"  📞 {name}: {phonebook[name]}")
    else:
        print(f"  ❌ '{name}' not found.")

def display_all():
    if not phonebook:
        print("  Phone book is empty.")
    else:
        print(f"\n  {'Name':<15} {'Number'}")
        print("  " + "-" * 30)
        for name, number in phonebook.items():
            print(f"  {name:<15} {number}")

# Test
add_contact("Alice",   "9876543210")
add_contact("Bob",     "9123456789")
add_contact("Charlie", "9000011111")

display_all()

print()
search_contact("Bob")
search_contact("Diana")
```

**Output:**
```
  ✅ 'Alice' added.
  ✅ 'Bob' added.
  ✅ 'Charlie' added.

  Name            Number
  ------------------------------
  Alice           9876543210
  Bob             9123456789
  Charlie         9000011111

  📞 Bob: 9123456789
  ❌ 'Diana' not found.
```

---

### 🟢 P3. Count Frequency of Each Word in a Sentence

**📝 Problem:**
Take a sentence from the user and count how many times each word appears using a dictionary.

✅ **Solution:**

```python
sentence = input("Enter a sentence: ").lower()

words = sentence.split()

word_count = {}

for word in words:
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1

print("\nWord Frequencies:")
print(f"  {'Word':<15} {'Count'}")
print("  " + "-" * 22)

for word, count in word_count.items():
    print(f"  {word:<15} {count}")
```

**Output:**
```
Enter a sentence: the cat sat on the mat and the cat

Word Frequencies:
  Word            Count
  ----------------------
  the             3
  cat             2
  sat             1
  on              1
  mat             1
  and             1
```

---

### 🟢 P4. Merge Two Dictionaries

**📝 Problem:**
Create two dictionaries. Merge them into one. If a key exists in both, keep the value from the second dictionary.

✅ **Solution:**

```python
dict1 = {"a": 1, "b": 2, "c": 3}
dict2 = {"c": 99, "d": 4, "e": 5}

print("Dict 1:", dict1)
print("Dict 2:", dict2)

# Method 1: Using update()
merged = dict1.copy()
merged.update(dict2)

print("\nMerged Dict:", merged)
print("Note: key 'c' from dict2 (99) overwrote dict1 value (3)")

# Show what was overwritten
print("\nOverwritten Keys:")
for key in dict1:
    if key in dict2:
        print(f"  '{key}': dict1={dict1[key]} → dict2={dict2[key]}")
```

**Output:**
```
Dict 1: {'a': 1, 'b': 2, 'c': 3}
Dict 2: {'c': 99, 'd': 4, 'e': 5}

Merged Dict: {'a': 1, 'b': 2, 'c': 99, 'd': 4, 'e': 5}
Note: key 'c' from dict2 (99) overwrote dict1 value (3)

Overwritten Keys:
  'c': dict1=3 → dict2=99
```

---

### 🟡 P5. Student Grade Book

**📝 Problem:**
Create a grade book using a dictionary. Store student name and marks. Display grades and find the topper.

✅ **Solution:**

```python
gradebook = {}

n = int(input("Enter number of students: "))

for i in range(n):
    name  = input(f"  Student {i + 1} Name  : ")
    marks = float(input(f"  Student {i + 1} Marks : "))
    gradebook[name] = marks

def get_grade(marks):
    if marks >= 90: return "A+"
    elif marks >= 80: return "A"
    elif marks >= 70: return "B"
    elif marks >= 60: return "C"
    elif marks >= 40: return "D"
    else:             return "F"

print(f"\n  {'Name':<12} {'Marks':>6} {'Grade':>6} {'Result'}")
print("  " + "-" * 35)

for name, marks in gradebook.items():
    grade  = get_grade(marks)
    result = "PASS" if grade != "F" else "FAIL"
    print(f"  {name:<12} {marks:>6.1f} {grade:>6}  {result}")

# Find topper
topper       = None
highest_mark = -1

for name, marks in gradebook.items():
    if marks > highest_mark:
        highest_mark = marks
        topper       = name

print(f"\n🏆 Topper: {topper} ({highest_mark})")
```

**Output:**
```
Enter number of students: 4
  Student 1 Name  : Alice
  Student 1 Marks : 92
  Student 2 Name  : Bob
  Student 2 Marks : 55
  Student 3 Name  : Charlie
  Student 3 Marks : 78
  Student 4 Name  : Diana
  Student 4 Marks : 35

  Name          Marks  Grade  Result
  -----------------------------------
  Alice          92.0    A+   PASS
  Bob            55.0     C   PASS
  Charlie        78.0     B   PASS
  Diana          35.0     F   FAIL

🏆 Topper: Alice (92.0)
```

---

### 🟡 P6. Inventory System

**📝 Problem:**
Create an inventory using a dictionary. Perform: Add item, Update quantity, Remove item, Display all with low stock warning.

✅ **Solution:**

```python
inventory    = {}
LOW_STOCK    = 5

def add_item(name, qty):
    if name in inventory:
        print(f"  ⚠️  '{name}' exists. Use update.")
    else:
        inventory[name] = qty
        print(f"  ✅ '{name}' added — Qty: {qty}")

def update_item(name, qty):
    if name in inventory:
        inventory[name] = qty
        print(f"  ✅ '{name}' updated — New Qty: {qty}")
    else:
        print(f"  ❌ '{name}' not found.")

def remove_item(name):
    if name in inventory:
        del inventory[name]
        print(f"  🗑️  '{name}' removed.")
    else:
        print(f"  ❌ '{name}' not found.")

def display_inventory():
    print(f"\n  {'Item':<15} {'Qty':>6}  {'Status'}")
    print("  " + "-" * 32)
    for name, qty in inventory.items():
        status = "⚠️ LOW STOCK" if qty <= LOW_STOCK else "OK"
        print(f"  {name:<15} {qty:>6}  {status}")

# Test
add_item("Apples",  50)
add_item("Bananas",  4)
add_item("Milk",    15)
add_item("Bread",    3)
add_item("Eggs",    24)

display_inventory()

print()
update_item("Milk", 2)
remove_item("Eggs")
remove_item("Sugar")

display_inventory()
```

**Output:**
```
  ✅ 'Apples' added — Qty: 50
  ✅ 'Bananas' added — Qty: 4
  ✅ 'Milk' added — Qty: 15
  ✅ 'Bread' added — Qty: 3
  ✅ 'Eggs' added — Qty: 24

  Item              Qty  Status
  --------------------------------
  Apples             50  OK
  Bananas             4  ⚠️ LOW STOCK
  Milk               15  OK
  Bread               3  ⚠️ LOW STOCK
  Eggs               24  OK

  ✅ 'Milk' updated — New Qty: 2
  🗑️  'Eggs' removed.
  ❌ 'Sugar' not found.

  Item              Qty  Status
  --------------------------------
  Apples             50  OK
  Bananas             4  ⚠️ LOW STOCK
  Milk                2  ⚠️ LOW STOCK
  Bread               3  ⚠️ LOW STOCK
```

---

### 🟡 P7. Word Frequency Counter From a Paragraph

**📝 Problem:**
Take a paragraph as input. Count word frequencies, display top 3 most used words.

✅ **Solution:**

```python
paragraph = input("Enter a paragraph:\n> ").lower()

# Remove basic punctuation
for char in ".,!?;:":
    paragraph = paragraph.replace(char, "")

words      = paragraph.split()
word_count = {}

for word in words:
    word_count[word] = word_count.get(word, 0) + 1

# Sort by frequency descending
sorted_words = sorted(word_count.items(),
                      key=lambda x: x[1],
                      reverse=True)

print(f"\nTotal Words  : {len(words)}")
print(f"Unique Words : {len(word_count)}")

print("\nAll Word Frequencies:")
print(f"  {'Word':<15} {'Count'}")
print("  " + "-" * 22)
for word, count in sorted_words:
    print(f"  {word:<15} {count}")

print("\nTop 3 Most Used Words:")
for i, (word, count) in enumerate(sorted_words[:3], 1):
    print(f"  {i}. '{word}' → {count} times")
```

**Output:**
```
Enter a paragraph:
> Python is great. Python is easy to learn. I love Python and Python is fun.

Total Words  : 15
Unique Words : 9

All Word Frequencies:
  Word            Count
  ----------------------
  python          4
  is              3
  great           1
  easy            1
  to              1
  learn           1
  i               1
  love            1
  and             1
  fun             1

Top 3 Most Used Words:
  1. 'python' → 4 times
  2. 'is' → 3 times
  3. 'great' → 1 times
```

---

### 🟡 P8. Find Key With Maximum Value

**📝 Problem:**
Create a dictionary of players and their scores. Find the player with the highest score without using max().

✅ **Solution:**

```python
scores = {}

n = int(input("Enter number of players: "))

for i in range(n):
    name  = input(f"  Player {i + 1} Name  : ")
    score = int(input(f"  Player {i + 1} Score : "))
    scores[name] = score

# Find max manually
top_player = None
top_score  = -1

for player, score in scores.items():
    if score > top_score:
        top_score  = score
        top_player = player

print(f"\n  {'Player':<15} {'Score':>6}")
print("  " + "-" * 23)
for player, score in scores.items():
    marker = " 🏆" if player == top_player else ""
    print(f"  {player:<15} {score:>6}{marker}")

print(f"\nTop Scorer: {top_player} with {top_score} points")
```

**Output:**
```
Enter number of players: 4
  Player 1 Name  : Alice
  Player 1 Score : 88
  Player 2 Name  : Bob
  Player 2 Score : 95
  Player 3 Name  : Charlie
  Player 3 Score : 72
  Player 4 Name  : Diana
  Player 4 Score : 91

  Player          Score
  -----------------------
  Alice              88
  Bob                95 🏆
  Charlie            72
  Diana              91

Top Scorer: Bob with 95 points
```

---

---

## ⚙️ Section 3: Functions

---

### 🟢 P1. Check Even or Odd

**📝 Problem:**
Write a function that takes a number as input and returns whether it is even or odd.

✅ **Solution:**

```python
def check_even_odd(n):
    if n % 2 == 0:
        return "Even"
    else:
        return "Odd"

# Test with multiple numbers
numbers = [1, 2, 7, 10, 33, 100, 0, -4]

for num in numbers:
    result = check_even_odd(num)
    print(f"  {num:>4} → {result}")
```

**Output:**
```
     1 → Odd
     2 → Even
     7 → Odd
    10 → Even
    33 → Odd
   100 → Even
     0 → Even
    -4 → Even
```

💡 `0 % 2 == 0` so zero is even. Negative even numbers also return `Even`.

---

### 🟢 P2. Largest of Three Numbers

**📝 Problem:**
Write a function that accepts three numbers and returns the largest one.

✅ **Solution:**

```python
def largest_of_three(a, b, c):
    if a >= b and a >= c:
        return a
    elif b >= a and b >= c:
        return b
    else:
        return c

# Take input from user
a = float(input("Enter first number  : "))
b = float(input("Enter second number : "))
c = float(input("Enter third number  : "))

result = largest_of_three(a, b, c)
print(f"\nLargest of ({a}, {b}, {c}) = {result}")
```

**Output:**
```
Enter first number  : 45
Enter second number : 78
Enter third number  : 33

Largest of (45.0, 78.0, 33.0) = 78.0
```

---

### 🟢 P3. Celsius to Fahrenheit Converter

**📝 Problem:**
Write a function that converts a temperature from Celsius to Fahrenheit and also Fahrenheit to Celsius.

✅ **Solution:**

```python
def celsius_to_fahrenheit(c):
    return (c * 9 / 5) + 32

def fahrenheit_to_celsius(f):
    return (f - 32) * 5 / 9

# Display conversion table
print(f"  {'Celsius':>10} {'Fahrenheit':>12}")
print("  " + "-" * 25)

for c in [0, 10, 20, 37, 100]:
    f = celsius_to_fahrenheit(c)
    print(f"  {c:>10}°C   {f:>10.2f}°F")

print()

# Take input from user
temp = float(input("Enter temperature   : "))
unit = input("Enter unit (C/F)    : ").strip().upper()

if unit == "C":
    result = celsius_to_fahrenheit(temp)
    print(f"{temp}°C = {result:.2f}°F")
elif unit == "F":
    result = fahrenheit_to_celsius(temp)
    print(f"{temp}°F = {result:.2f}°C")
else:
    print("Invalid unit.")
```

**Output:**
```
    Celsius   Fahrenheit
  -------------------------
         0°C        32.00°F
        10°C        50.00°F
        20°C        68.00°F
        37°C        98.60°F
       100°C       212.00°F

Enter temperature   : 37
Enter unit (C/F)    : C
37.0°C = 98.60°F
```

---

### 🟢 P4. Leap Year Checker

**📝 Problem:**
Write a function to check if a given year is a leap year or not.

✅ **Solution:**

```python
def is_leap_year(year):
    # A year is a leap year if:
    # Divisible by 4 AND (not divisible by 100 OR divisible by 400)
    if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
        return True
    return False

# Take input
year = int(input("Enter a year: "))

if is_leap_year(year):
    print(f"{year} is a Leap Year ✅")
else:
    print(f"{year} is NOT a Leap Year ❌")

# Show a range of leap years
print("\nLeap years from 2000 to 2030:")
leaps = []
for y in range(2000, 2031):
    if is_leap_year(y):
        leaps.append(y)

print(leaps)
```

**Output:**
```
Enter a year: 2024
2024 is a Leap Year ✅

Leap years from 2000 to 2030:
[2000, 2004, 2008, 2012, 2016, 2020, 2024, 2028]
```

💡 **Rule:** Divisible by 4 → leap. But divisible by 100 → NOT leap. But divisible by 400 → leap again. (e.g., 1900 is NOT, 2000 IS)

---

### 🟡 P5. Fibonacci Series Up to N

**📝 Problem:**
Write a function to generate the Fibonacci series up to n terms. Return the series as a list.

✅ **Solution:**

```python
def fibonacci(n):
    if n <= 0:
        return []
    elif n == 1:
        return [0]

    series = [0, 1]

    for i in range(2, n):
        next_num = series[i - 1] + series[i - 2]    # Sum of last two
        series.append(next_num)

    return series

n = int(input("Enter number of terms: "))

series = fibonacci(n)

print(f"\nFibonacci Series ({n} terms):")
print(series)

print("\nFormatted:")
for i, num in enumerate(series, 1):
    print(f"  Term {i:2}: {num}")
```

**Output:**
```
Enter number of terms: 8

Fibonacci Series (8 terms):
[0, 1, 1, 2, 3, 5, 8, 13]

Formatted:
  Term  1: 0
  Term  2: 1
  Term  3: 1
  Term  4: 2
  Term  5: 3
  Term  6: 5
  Term  7: 8
  Term  8: 13
```

💡 Each term = sum of the two previous terms. First two terms are always `0` and `1`.

---

### 🟡 P6. Count Digits, Letters, Spaces in a String

**📝 Problem:**
Write a function that takes a string and returns the count of digits, letters, and spaces separately.

✅ **Solution:**

```python
def analyze_string(text):
    letters = 0
    digits  = 0
    spaces  = 0
    others  = 0

    for char in text:
        if char.isalpha():
            letters += 1
        elif char.isdigit():
            digits += 1
        elif char == " ":
            spaces += 1
        else:
            others += 1

    return letters, digits, spaces, others

text = input("Enter a string: ")

letters, digits, spaces, others = analyze_string(text)

print(f"\nString  : '{text}'")
print(f"Letters : {letters}")
print(f"Digits  : {digits}")
print(f"Spaces  : {spaces}")
print(f"Others  : {others}")
print(f"Total   : {len(text)}")
```

**Output:**
```
Enter a string: Hello World 123!

String  : 'Hello World 123!'
Letters : 10
Digits  : 3
Spaces  : 2
Others  : 1
Total   : 16
```

---

### 🟡 P7. Function Using *args — Min, Max, Sum, Average

**📝 Problem:**
Write a function using `*args` that accepts any number of values and returns their minimum, maximum, sum, and average.

✅ **Solution:**

```python
def analyze(*args):
    if not args:
        return None

    total   = 0
    minimum = args[0]
    maximum = args[0]

    for num in args:
        total += num
        if num < minimum:
            minimum = num
        if num > maximum:
            maximum = num

    average = total / len(args)

    return minimum, maximum, total, round(average, 2)

# Test with different number of arguments
print("── Test 1: (3 numbers) ──────────────")
mn, mx, sm, avg = analyze(10, 50, 30)
print(f"  Min: {mn} | Max: {mx} | Sum: {sm} | Avg: {avg}")

print("\n── Test 2: (6 numbers) ──────────────")
mn, mx, sm, avg = analyze(5, 15, 25, 35, 45, 55)
print(f"  Min: {mn} | Max: {mx} | Sum: {sm} | Avg: {avg}")

print("\n── Test 3: (user input) ─────────────")
nums   = input("  Enter numbers separated by space: ")
values = [float(x) for x in nums.split()]
mn, mx, sm, avg = analyze(*values)
print(f"  Min: {mn} | Max: {mx} | Sum: {sm} | Avg: {avg}")
```

**Output:**
```
── Test 1: (3 numbers) ──────────────
  Min: 10 | Max: 50 | Sum: 90 | Avg: 30.0

── Test 2: (6 numbers) ──────────────
  Min: 5 | Max: 55 | Sum: 180 | Avg: 30.0

── Test 3: (user input) ─────────────
  Enter numbers separated by space: 12 45 7 89 23
  Min: 7.0 | Max: 89.0 | Sum: 176.0 | Avg: 35.2
```

💡 `*args` collects all positional arguments as a **tuple** — you can pass 2 or 200 values with the same function.

---

### 🟡 P8. Armstrong Number Checker

**📝 Problem:**
Write a function to check if a number is an Armstrong number. An Armstrong number equals the sum of its own digits each raised to the power of the number of digits. (e.g., 153 = 1³ + 5³ + 3³)

✅ **Solution:**

```python
def is_armstrong(n):
    digits     = str(n)
    num_digits = len(digits)
    total      = 0

    for d in digits:
        total += int(d) ** num_digits    # Each digit ^ count of digits

    return total == n

# Single check
num = int(input("Enter a number: "))

if is_armstrong(num):
    print(f"{num} is an Armstrong Number ✅")
else:
    print(f"{num} is NOT an Armstrong Number ❌")

# Display all Armstrong numbers up to 1000
print("\nArmstrong Numbers from 1 to 1000:")
armstrong_list = []
for i in range(1, 1001):
    if is_armstrong(i):
        armstrong_list.append(i)

print(armstrong_list)
```

**Output:**
```
Enter a number: 153
153 is an Armstrong Number ✅

Armstrong Numbers from 1 to 1000:
[1, 2, 3, 4, 5, 6, 7, 8, 9, 153, 370, 371, 407]
```

💡 153 = 1³ + 5³ + 3³ = 1 + 125 + 27 = 153 ✅

---

---

## 🏛️ Section 4: Classes & Objects

---

### 🟢 P1. Book Class

**📝 Problem:**
Create a `Book` class with attributes: title, author, price. Add a method to display book details and apply a discount.

✅ **Solution:**

```python
class Book:
    def __init__(self, title, author, price):
        self.title  = title
        self.author = author
        self.price  = price

    def display(self):
        print(f"  Title  : {self.title}")
        print(f"  Author : {self.author}")
        print(f"  Price  : ₹{self.price:.2f}")

    def apply_discount(self, percent):
        discount    = (percent / 100) * self.price
        new_price   = self.price - discount
        print(f"  Discount: {percent}% off → ₹{new_price:.2f}")
        return new_price


# Create book objects
b1 = Book("Python Basics",   "John Smith",    499.00)
b2 = Book("Clean Code",      "Robert Martin", 799.00)
b3 = Book("Data Structures", "Alice Brown",   599.00)

books = [b1, b2, b3]

for book in books:
    print("\n── Book ──────────────────────")
    book.display()
    book.apply_discount(10)
```

**Output:**
```
── Book ──────────────────────
  Title  : Python Basics
  Author : John Smith
  Price  : ₹499.00
  Discount: 10% off → ₹449.10

── Book ──────────────────────
  Title  : Clean Code
  Author : Robert Martin
  Price  : ₹799.00
  Discount: 10% off → ₹719.10

── Book ──────────────────────
  Title  : Data Structures
  Author : Alice Brown
  Price  : ₹599.00
  Discount: 10% off → ₹539.10
```

---

### 🟢 P2. Student Class — Pass or Fail

**📝 Problem:**
Create a `Student` class with name, roll number, and marks. Add a method to check whether the student passed or failed (pass mark = 40).

✅ **Solution:**

```python
class Student:
    pass_mark = 40     # Class attribute

    def __init__(self, name, roll, marks):
        self.name  = name
        self.roll  = roll
        self.marks = marks

    def result(self):
        if self.marks >= Student.pass_mark:
            return "PASS ✅"
        else:
            return "FAIL ❌"

    def display(self):
        print(f"  Roll   : {self.roll}")
        print(f"  Name   : {self.name}")
        print(f"  Marks  : {self.marks}")
        print(f"  Result : {self.result()}")
        print()


# Create student objects
students = [
    Student("Alice",   101, 78),
    Student("Bob",     102, 35),
    Student("Charlie", 103, 40),
    Student("Diana",   104, 92),
]

for student in students:
    student.display()
```

**Output:**
```
  Roll   : 101
  Name   : Alice
  Marks  : 78
  Result : PASS ✅

  Roll   : 102
  Name   : Bob
  Marks  : 35
  Result : FAIL ❌

  Roll   : 103
  Name   : Charlie
  Marks  : 40
  Result : PASS ✅

  Roll   : 104
  Name   : Diana
  Marks  : 92
  Result : PASS ✅
```

---

### 🟢 P3. Rectangle Class

**📝 Problem:**
Create a `Rectangle` class with width and height. Add methods to calculate area and perimeter. Add a method to check if it is a square.

✅ **Solution:**

```python
class Rectangle:
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def is_square(self):
        return self.width == self.height

    def display(self):
        print(f"  Width     : {self.width}")
        print(f"  Height    : {self.height}")
        print(f"  Area      : {self.area()}")
        print(f"  Perimeter : {self.perimeter()}")
        print(f"  Is Square : {'Yes ✅' if self.is_square() else 'No ❌'}")
        print()


# Test
r1 = Rectangle(5, 10)
r2 = Rectangle(7, 7)
r3 = Rectangle(3, 8)

for r in [r1, r2, r3]:
    r.display()
```

**Output:**
```
  Width     : 5
  Height    : 10
  Area      : 50
  Perimeter : 30
  Is Square : No ❌

  Width     : 7
  Height    : 7
  Area      : 49
  Perimeter : 28
  Is Square : Yes ✅

  Width     : 3
  Height    : 8
  Area      : 24
  Perimeter : 22
  Is Square : No ❌
```

---

### 🟢 P4. Counter Class

**📝 Problem:**
Create a `Counter` class. Add methods to increment, decrement, reset, and display the current count. Prevent count from going below zero.

✅ **Solution:**

```python
class Counter:
    def __init__(self, start=0):
        self.count = start

    def increment(self, by=1):
        self.count += by
        print(f"  ++ Count: {self.count}")

    def decrement(self, by=1):
        if self.count - by < 0:
            print(f"  ⚠️  Cannot go below 0. Count stays: {self.count}")
        else:
            self.count -= by
            print(f"  -- Count: {self.count}")

    def reset(self):
        self.count = 0
        print(f"  🔄 Counter reset to 0")

    def display(self):
        print(f"  Current Count: {self.count}")


# Test
c = Counter()

c.display()

c.increment()
c.increment()
c.increment(5)
c.display()

c.decrement(3)
c.decrement(10)    # Below zero → blocked
c.display()

c.reset()
c.display()
```

**Output:**
```
  Current Count: 0
  ++ Count: 1
  ++ Count: 2
  ++ Count: 7
  Current Count: 7
  -- Count: 4
  ⚠️  Cannot go below 0. Count stays: 4
  Current Count: 4
  🔄 Counter reset to 0
  Current Count: 0
```

---

### 🟡 P5. BankAccount Class — Deposit, Withdraw, Statement

**📝 Problem:**
Create a `BankAccount` class. Add deposit, withdraw methods. Maintain a transaction history and display a full account statement.

✅ **Solution:**

```python
class BankAccount:
    def __init__(self, holder, account_no, balance=0):
        self.holder      = holder
        self.account_no  = account_no
        self.balance     = balance
        self.transactions = []

    def deposit(self, amount):
        if amount <= 0:
            print("  ❌ Invalid deposit amount.")
            return
        self.balance += amount
        self.transactions.append(("Deposit",    amount, self.balance))
        print(f"  ✅ Deposited ₹{amount} | Balance: ₹{self.balance}")

    def withdraw(self, amount):
        if amount <= 0:
            print("  ❌ Invalid withdrawal amount.")
        elif amount > self.balance:
            print(f"  ❌ Insufficient balance! Available: ₹{self.balance}")
        else:
            self.balance -= amount
            self.transactions.append(("Withdraw", amount, self.balance))
            print(f"  ✅ Withdrew ₹{amount} | Balance: ₹{self.balance}")

    def statement(self):
        print(f"\n  ══════════════════════════════════════")
        print(f"  Account Holder : {self.holder}")
        print(f"  Account No     : {self.account_no}")
        print(f"  ══════════════════════════════════════")
        print(f"  {'Type':<12} {'Amount':>10} {'Balance':>10}")
        print(f"  {'-'*36}")
        for t_type, amount, bal in self.transactions:
            print(f"  {t_type:<12} ₹{amount:>8} ₹{bal:>8}")
        print(f"  {'-'*36}")
        print(f"  Current Balance : ₹{self.balance}")
        print(f"  ══════════════════════════════════════")


# Test
acc = BankAccount("Alice", "ACC-1001", 1000)

acc.deposit(500)
acc.withdraw(200)
acc.deposit(1000)
acc.withdraw(3000)    # Insufficient
acc.withdraw(800)

acc.statement()
```

**Output:**
```
  ✅ Deposited ₹500 | Balance: ₹1500
  ✅ Withdrew ₹200 | Balance: ₹1300
  ✅ Deposited ₹1000 | Balance: ₹2300
  ❌ Insufficient balance! Available: ₹2300
  ✅ Withdrew ₹800 | Balance: ₹1500

  ══════════════════════════════════════
  Account Holder : Alice
  Account No     : ACC-1001
  ══════════════════════════════════════
  Type           Amount    Balance
  ------------------------------------
  Deposit       ₹   500   ₹  1500
  Withdraw      ₹   200   ₹  1300
  Deposit       ₹  1000   ₹  2300
  Withdraw      ₹   800   ₹  1500
  ------------------------------------
  Current Balance : ₹1500
  ══════════════════════════════════════
```

---

### 🟡 P6. Vehicle → Car Inheritance

**📝 Problem:**
Create a `Vehicle` base class with brand and speed. Create a `Car` child class that inherits from it and adds fuel type and number of doors.

✅ **Solution:**

```python
class Vehicle:
    def __init__(self, brand, speed):
        self.brand = brand
        self.speed = speed

    def move(self):
        return f"{self.brand} is moving at {self.speed} km/h."

    def stop(self):
        return f"{self.brand} has stopped."

    def display(self):
        print(f"  Brand : {self.brand}")
        print(f"  Speed : {self.speed} km/h")


class Car(Vehicle):
    def __init__(self, brand, speed, fuel, doors):
        super().__init__(brand, speed)    # Call Vehicle's __init__
        self.fuel  = fuel
        self.doors = doors

    def honk(self):
        return f"{self.brand} goes: Beep Beep! 🚗"

    def display(self):
        super().display()                 # Call parent display()
        print(f"  Fuel  : {self.fuel}")
        print(f"  Doors : {self.doors}")


# Test
v1 = Vehicle("Generic Vehicle", 80)
c1 = Car("Toyota Camry",    120, "Petrol",   4)
c2 = Car("Tesla Model 3",   200, "Electric", 4)

print("── Vehicle ───────────────────────")
v1.display()
print(f"  {v1.move()}")

print("\n── Car 1 ─────────────────────────")
c1.display()
print(f"  {c1.move()}")
print(f"  {c1.honk()}")

print("\n── Car 2 ─────────────────────────")
c2.display()
print(f"  {c2.move()}")

print("\n── Inheritance Check ─────────────")
print(f"  Car is Vehicle? {isinstance(c1, Vehicle)}")
print(f"  Vehicle is Car? {isinstance(v1, Car)}")
```

**Output:**
```
── Vehicle ───────────────────────
  Brand : Generic Vehicle
  Speed : 80 km/h
  Generic Vehicle is moving at 80 km/h.

── Car 1 ─────────────────────────
  Brand : Toyota Camry
  Speed : 120 km/h
  Fuel  : Petrol
  Doors : 4
  Toyota Camry is moving at 120 km/h.
  Toyota Camry goes: Beep Beep! 🚗

── Car 2 ─────────────────────────
  Brand : Tesla Model 3
  Speed : 200 km/h
  Fuel  : Electric
  Doors : 4
  Tesla Model 3 is moving at 200 km/h.

── Inheritance Check ─────────────
  Car is Vehicle? True
  Vehicle is Car? False
```

---

### 🟡 P7. Employee Class — Salary With Bonus

**📝 Problem:**
Create an `Employee` class with name, ID, and base salary. Add methods to calculate bonus (20% of salary) and total pay, and display a salary slip.

✅ **Solution:**

```python
class Employee:
    def __init__(self, emp_id, name, department, base_salary):
        self.emp_id      = emp_id
        self.name        = name
        self.department  = department
        self.base_salary = base_salary

    def calculate_bonus(self):
        return self.base_salary * 0.20

    def calculate_total(self):
        return self.base_salary + self.calculate_bonus()

    def salary_slip(self):
        bonus = self.calculate_bonus()
        total = self.calculate_total()

        print(f"  ╔══════════════════════════════════╗")
        print(f"  ║         SALARY SLIP              ║")
        print(f"  ╠══════════════════════════════════╣")
        print(f"  ║  ID         : {self.emp_id:<18}║")
        print(f"  ║  Name       : {self.name:<18}║")
        print(f"  ║  Department : {self.department:<18}║")
        print(f"  ╠══════════════════════════════════╣")
        print(f"  ║  Base Salary: ₹{self.base_salary:<17,}║")
        print(f"  ║  Bonus (20%): ₹{bonus:<17,.2f}║")
        print(f"  ║  Total Pay  : ₹{total:<17,.2f}║")
        print(f"  ╚══════════════════════════════════╝")
        print()


# Create employees
employees = [
    Employee("E001", "Alice",   "IT",      60000),
    Employee("E002", "Bob",     "HR",      45000),
    Employee("E003", "Charlie", "Finance", 75000),
]

for emp in employees:
    emp.salary_slip()
```

**Output:**
```
  ╔══════════════════════════════════╗
  ║         SALARY SLIP              ║
  ╠══════════════════════════════════╣
  ║  ID         : E001               ║
  ║  Name       : Alice              ║
  ║  Department : IT                 ║
  ╠══════════════════════════════════╣
  ║  Base Salary: ₹60,000            ║
  ║  Bonus (20%): ₹12,000.00         ║
  ║  Total Pay  : ₹72,000.00         ║
  ╚══════════════════════════════════╝
  ...
```

---

### 🟡 P8. Library Class — Add, Remove, Search Books

**📝 Problem:**
Create a `Library` class that manages a collection of books. Add methods to add a book, remove a book, search by title, and display all books.

✅ **Solution:**

```python
class Library:
    def __init__(self, name):
        self.name  = name
        self.books = []

    def add_book(self, title, author):
        book = {"title": title, "author": author}
        self.books.append(book)
        print(f"  ✅ Added: '{title}' by {author}")

    def remove_book(self, title):
        for book in self.books:
            if book["title"].lower() == title.lower():
                self.books.remove(book)
                print(f"  🗑️  Removed: '{title}'")
                return
        print(f"  ❌ '{title}' not found.")

    def search_book(self, keyword):
        results = []
        for book in self.books:
            if keyword.lower() in book["title"].lower() \
            or keyword.lower() in book["author"].lower():
                results.append(book)
        return results

    def display_all(self):
        print(f"\n  📚 {self.name} — {len(self.books)} book(s)")
        if not self.books:
            print("  (No books available)")
        else:
            print(f"  {'#':<4} {'Title':<25} {'Author'}")
            print("  " + "-" * 45)
            for i, book in enumerate(self.books, 1):
                print(f"  {i:<4} {book['title']:<25} {book['author']}")


# Test
lib = Library("City Library")

lib.add_book("Python Basics",    "John Smith")
lib.add_book("Clean Code",       "Robert Martin")
lib.add_book("Linux Essentials", "Alice Brown")
lib.add_book("Python Advanced",  "John Smith")

lib.display_all()

print("\n🔍 Search: 'Python'")
results = lib.search_book("Python")
for r in results:
    print(f"  → '{r['title']}' by {r['author']}")

print("\n🔍 Search: 'John Smith'")
results = lib.search_book("John Smith")
for r in results:
    print(f"  → '{r['title']}' by {r['author']}")

print()
lib.remove_book("Clean Code")
lib.remove_book("Unknown Book")

lib.display_all()
```

**Output:**
```
  ✅ Added: 'Python Basics' by John Smith
  ✅ Added: 'Clean Code' by Robert Martin
  ✅ Added: 'Linux Essentials' by Alice Brown
  ✅ Added: 'Python Advanced' by John Smith

  📚 City Library — 4 book(s)
  #    Title                     Author
  ---------------------------------------------
  1    Python Basics             John Smith
  2    Clean Code                Robert Martin
  3    Linux Essentials          Alice Brown
  4    Python Advanced           John Smith

🔍 Search: 'Python'
  → 'Python Basics' by John Smith
  → 'Python Advanced' by John Smith

🔍 Search: 'John Smith'
  → 'Python Basics' by John Smith
  → 'Python Advanced' by John Smith

  🗑️  Removed: 'Clean Code'
  ❌ 'Unknown Book' not found.

  📚 City Library — 3 book(s)
  #    Title                     Author
  ---------------------------------------------
  1    Python Basics             John Smith
  2    Linux Essentials          Alice Brown
  3    Python Advanced           John Smith
```

---

---

## 🌐 Section 5: Sockets

> ⚠️ Run the **Server file first** in one terminal, then run the **Client file** in a second terminal.

---

### 🟢 P1. Client Sends Name → Server Greets Back

**📝 Problem:**
Client sends their name to the server. Server receives the name and sends back a greeting message.

✅ **Solution:**

```python
# ══ FILE: server_p1.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6001

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Waiting on port {PORT}...")

conn, addr = server.accept()
print(f"[SERVER] Connected: {addr}")

# Receive name from client
name = conn.recv(1024).decode()
print(f"[SERVER] Received name: {name}")

# Send greeting back
greeting = f"Hello {name}! Welcome to the server."
conn.send(greeting.encode())
print(f"[SERVER] Greeting sent.")

conn.close()
server.close()
```

```python
# ══ FILE: client_p1.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6001

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

# Send name to server
name = input("[CLIENT] Enter your name: ")
client.send(name.encode())

# Receive greeting from server
response = client.recv(1024).decode()
print(f"[SERVER]: {response}")

client.close()
```

**Output:**
```
── Server Terminal ──────────────────
[SERVER] Waiting on port 6001...
[SERVER] Connected: ('127.0.0.1', 54401)
[SERVER] Received name: Alice
[SERVER] Greeting sent.

── Client Terminal ──────────────────
[CLIENT] Enter your name: Alice
[SERVER]: Hello Alice! Welcome to the server.
```

---

### 🟢 P2. Client Sends Two Numbers → Server Returns Sum

**📝 Problem:**
Client sends two numbers to the server. Server calculates their sum and sends the result back.

✅ **Solution:**

```python
# ══ FILE: server_p2.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6002

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Waiting on port {PORT}...")

conn, addr = server.accept()
print(f"[SERVER] Connected: {addr}")

# Receive two numbers (sent as "num1,num2")
data = conn.recv(1024).decode()
print(f"[SERVER] Received: {data}")

parts = data.split(",")
num1  = float(parts[0])
num2  = float(parts[1])

# Calculate
total = num1 + num2
response = f"{num1} + {num2} = {total}"

conn.send(response.encode())
print(f"[SERVER] Sent: {response}")

conn.close()
server.close()
```

```python
# ══ FILE: client_p2.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6002

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

# Get two numbers from user
num1 = input("[CLIENT] Enter first number  : ")
num2 = input("[CLIENT] Enter second number : ")

# Send as "num1,num2"
message = f"{num1},{num2}"
client.send(message.encode())

# Receive result
result = client.recv(1024).decode()
print(f"[SERVER]: {result}")

client.close()
```

**Output:**
```
── Server Terminal ──────────────────
[SERVER] Waiting on port 6002...
[SERVER] Connected: ('127.0.0.1', 54402)
[SERVER] Received: 25,75
[SERVER] Sent: 25.0 + 75.0 = 100.0

── Client Terminal ──────────────────
[CLIENT] Enter first number  : 25
[CLIENT] Enter second number : 75
[SERVER]: 25.0 + 75.0 = 100.0
```

💡 We send both numbers as a **comma-separated string** and split it on the server side.

---

### 🟢 P3. Client Sends String → Server Returns Length

**📝 Problem:**
Client sends a string to the server. Server returns the number of characters (length) in the string.

✅ **Solution:**

```python
# ══ FILE: server_p3.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6003

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Waiting on port {PORT}...")

conn, addr = server.accept()
print(f"[SERVER] Connected: {addr}")

# Receive string
text = conn.recv(1024).decode()
print(f"[SERVER] Received: '{text}'")

# Calculate length and send back
length   = len(text)
response = f"Length of '{text}' = {length} characters"

conn.send(response.encode())
print(f"[SERVER] Sent: {response}")

conn.close()
server.close()
```

```python
# ══ FILE: client_p3.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6003

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

# Send string to server
text = input("[CLIENT] Enter a string: ")
client.send(text.encode())

# Receive length result
response = client.recv(1024).decode()
print(f"[SERVER]: {response}")

client.close()
```

**Output:**
```
── Server Terminal ──────────────────
[SERVER] Waiting on port 6003...
[SERVER] Connected: ('127.0.0.1', 54403)
[SERVER] Received: 'Hello Python'
[SERVER] Sent: Length of 'Hello Python' = 12 characters

── Client Terminal ──────────────────
[CLIENT] Enter a string: Hello Python
[SERVER]: Length of 'Hello Python' = 12 characters
```

---

### 🟡 P4. Client Sends Number → Server Checks Prime

**📝 Problem:**
Client sends a number to the server. Server checks if it is prime or not and sends the result back.

✅ **Solution:**

```python
# ══ FILE: server_p4.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6004

def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Prime Checker running on port {PORT}...")

conn, addr = server.accept()
print(f"[SERVER] Connected: {addr}")

# Receive number
data = conn.recv(1024).decode()
print(f"[SERVER] Received: {data}")

try:
    num = int(data)
    if is_prime(num):
        response = f"{num} is a Prime Number ✅"
    else:
        response = f"{num} is NOT a Prime Number ❌"
except ValueError:
    response = "ERROR: Invalid number received."

conn.send(response.encode())
print(f"[SERVER] Sent: {response}")

conn.close()
server.close()
```

```python
# ══ FILE: client_p4.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6004

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print("[CLIENT] Connected to Prime Checker Server.")

# Send number
num = input("[CLIENT] Enter a number to check: ")
client.send(num.encode())

# Receive result
result = client.recv(1024).decode()
print(f"[SERVER]: {result}")

client.close()
```

**Output:**
```
── Server Terminal ──────────────────
[SERVER] Prime Checker running on port 6004...
[SERVER] Connected: ('127.0.0.1', 54404)
[SERVER] Received: 17
[SERVER] Sent: 17 is a Prime Number ✅

── Client Terminal ──────────────────
[CLIENT] Connected to Prime Checker Server.
[CLIENT] Enter a number to check: 17
[SERVER]: 17 is a Prime Number ✅
```

---

### 🟡 P5. Client Sends Sentence → Server Returns Word Count

**📝 Problem:**
Client sends a sentence to the server. Server returns total word count, character count, and the longest word.

✅ **Solution:**

```python
# ══ FILE: server_p5.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6005

def analyze_sentence(sentence):
    words       = sentence.split()
    word_count  = len(words)
    char_count  = len(sentence)
    char_no_sp  = len(sentence.replace(" ", ""))

    # Find longest word
    longest = ""
    for word in words:
        if len(word) > len(longest):
            longest = word

    result = (
        f"\n  Sentence    : '{sentence}'\n"
        f"  Word Count  : {word_count}\n"
        f"  Char Count  : {char_count}\n"
        f"  Chars(no sp): {char_no_sp}\n"
        f"  Longest Word: '{longest}' ({len(longest)} chars)"
    )
    return result

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Sentence Analyzer on port {PORT}...")

conn, addr = server.accept()
print(f"[SERVER] Connected: {addr}")

sentence = conn.recv(4096).decode()
print(f"[SERVER] Received: '{sentence}'")

result = analyze_sentence(sentence)
conn.send(result.encode())
print("[SERVER] Analysis sent.")

conn.close()
server.close()
```

```python
# ══ FILE: client_p5.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6005

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print("[CLIENT] Connected to Sentence Analyzer.")

sentence = input("[CLIENT] Enter a sentence: ")
client.send(sentence.encode())

result = client.recv(4096).decode()
print(f"[SERVER] Analysis:{result}")

client.close()
```

**Output:**
```
── Server Terminal ──────────────────
[SERVER] Sentence Analyzer on port 6005...
[SERVER] Connected: ('127.0.0.1', 54405)
[SERVER] Received: 'Python programming is awesome'
[SERVER] Analysis sent.

── Client Terminal ──────────────────
[CLIENT] Connected to Sentence Analyzer.
[CLIENT] Enter a sentence: Python programming is awesome
[SERVER] Analysis:
  Sentence    : 'Python programming is awesome'
  Word Count  : 4
  Char Count  : 29
  Chars(no sp): 26
  Longest Word: 'programming' (11 chars)
```

---

### 🟡 P6. Multi-Message Chat With bye to Exit

**📝 Problem:**
Build a chat application. Server and client keep exchanging messages in a loop. Typing `bye` ends the connection on either side.

✅ **Solution:**

```python
# ══ FILE: server_p6.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6006

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)

print(f"[SERVER] Chat server ready on port {PORT}.")
print("[SERVER] Waiting for client...\n")

conn, addr = server.accept()
print(f"[SERVER] Client connected: {addr}")
print("[SERVER] Type 'bye' to end the chat.\n")

while True:
    # Receive from client first
    client_msg = conn.recv(1024).decode()

    if not client_msg or client_msg.lower() == "bye":
        print("[SERVER] Client has left the chat.")
        break

    print(f"[CLIENT]: {client_msg}")

    # Server replies
    server_msg = input("[SERVER]: ")
    conn.send(server_msg.encode())

    if server_msg.lower() == "bye":
        print("[SERVER] Ending chat.")
        break

conn.close()
server.close()
```

```python
# ══ FILE: client_p6.py ═══════════════════════════
import socket

HOST = 'localhost'
PORT = 6006

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

print("[CLIENT] Connected to chat server.")
print("[CLIENT] Type 'bye' to end the chat.\n")

while True:
    # Client sends first
    msg = input("[CLIENT]: ")
    client.send(msg.encode())

    if msg.lower() == "bye":
        print("[CLIENT] Disconnected.")
        break

    # Receive server reply
    server_reply = client.recv(1024).decode()

    if not server_reply or server_reply.lower() == "bye":
        print("[SERVER] Server has ended the chat.")
        break

    print(f"[SERVER]: {server_reply}")

client.close()
```

**Sample Chat Output:**
```
── Server Terminal ──────────────────────────────
[SERVER] Chat server ready on port 6006.
[SERVER] Waiting for client...

[SERVER] Client connected: ('127.0.0.1', 54410)
[SERVER] Type 'bye' to end the chat.

[CLIENT]: Hello Server!
[SERVER]: Hi! How can I help?
[CLIENT]: What is your port number?
[SERVER]: I am running on port 6006.
[CLIENT]: bye
[SERVER] Client has left the chat.

── Client Terminal ──────────────────────────────
[CLIENT] Connected to chat server.
[CLIENT] Type 'bye' to end the chat.

[CLIENT]: Hello Server!
[SERVER]: Hi! How can I help?
[CLIENT]: What is your port number?
[SERVER]: I am running on port 6006.
[CLIENT]: bye
[CLIENT] Disconnected.
```

💡 **Socket Quick Reference:**
```
SERVER                          CLIENT
──────────────────────────────────────
socket()   → Create             socket()   → Create
bind()     → Set IP & Port      connect()  → Connect to server
listen()   → Start listening    send()     → Send data
accept()   → Wait for client    recv()     → Get response
recv()     → Get data           close()    → Done
send()     → Send reply
close()    → Done
```

---

---

## 📊 Summary

| Section | Basic | Medium | Total |
|---|---|---|---|
| 📘 Lists | 4 | 4 | **8** |
| 📘 Dictionaries | 4 | 4 | **8** |
| ⚙️ Functions | 4 | 4 | **8** |
| 🏛️ Classes & Objects | 4 | 4 | **8** |
| 🌐 Sockets | 3 | 3 | **6** |
| | | **TOTAL** | **38** |

---

*📁 Python-Exam-Prep Series | PGCP-ITISS | February 2026*
*⬅️ Previous: [Part 4](Part4_FacultyAssignments.md)*
*🏠 Index: [README.md](README.md)*