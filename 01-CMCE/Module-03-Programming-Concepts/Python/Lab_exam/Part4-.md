# 🐍 Python Exam Prep — Part 4: Faculty Assignments & Programs

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Topics](https://img.shields.io/badge/Topics-8-green)
![Programs](https://img.shields.io/badge/Programs-28-orange)
![Level](https://img.shields.io/badge/Level-Faculty%20Assignment-yellow)

---

## 📌 Index

| # | Section | Source | Programs |
|---|---|---|---|
| 1 | [⚙️ Functions](#️-section-1-functions) | Assignment 3 | 5 |
| 2 | [📘 Lists](#-section-2-lists) | Assignment 3 + 4 | 7 |
| 3 | [📘 Tuples](#-section-3-tuples) | Assignment 4 | 2 |
| 4 | [📘 Dictionaries](#-section-4-dictionaries) | Assignment 4 | 2 |
| 5 | [📘 Sets](#-section-5-sets) | Assignment 4 | 1 |
| 6 | [📘 Strings](#-section-6-strings) | Added — Faculty Level | 4 |
| 7 | [🏛️ Classes & Objects](#️-section-7-classes--objects-oop) | Added — Faculty Level | 4 |
| 8 | [🌐 Sockets](#-section-8-sockets) | Faculty Class Programs | 3 |

---

## 🗺️ Legend

| Symbol | Meaning |
|---|---|
| ✅ | Guided Solution / Correct |
| 🐛 | Bug Found |
| 💡 | Key Tip |
| ⚠️ | Important Note |
| ❌ | Wrong Code / Bug Line |

---

---

## ⚙️ Section 1: Functions

> 📋 **Source:** Assignment 3 — Python Functions (5 Problems)

---

### P1. Factorial Using Recursion

**📝 Problem Statement:**
Write a function to calculate the factorial of a given number using recursion and return the result.

✅ **Guided Solution:**

```python
def factorial(n):
    # Base case: factorial of 0 or 1 is 1
    if n == 0 or n == 1:
        return 1
    # Recursive case: n! = n × (n-1)!
    return n * factorial(n - 1)

# Take input from user
num = int(input("Enter a number: "))

if num < 0:
    print("Factorial is not defined for negative numbers.")
else:
    result = factorial(num)
    print(f"Factorial of {num} = {result}")
```

**Output:**
```
Enter a number: 5
Factorial of 5 = 120
```

💡 **How recursion works for factorial(4):**
```
factorial(4)
→ 4 × factorial(3)
→ 4 × 3 × factorial(2)
→ 4 × 3 × 2 × factorial(1)
→ 4 × 3 × 2 × 1
→ 24
```

---

### P2. Prime Number Check

**📝 Problem Statement:**
Write a function that takes a number as input and returns whether it is a prime number or not.

✅ **Guided Solution:**

```python
def is_prime(n):
    # Numbers less than 2 are not prime
    if n < 2:
        return False

    # Check divisibility from 2 to square root of n
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False    # Found a divisor → not prime

    return True    # No divisors found → prime

# Take input from user
num = int(input("Enter a number: "))

if is_prime(num):
    print(f"{num} is a Prime Number ✅")
else:
    print(f"{num} is NOT a Prime Number ❌")
```

**Output:**
```
Enter a number: 17
17 is a Prime Number ✅

Enter a number: 15
15 is NOT a Prime Number ❌
```

💡 **Key Tip:** We only check up to `√n` because if `n` has a factor greater than `√n`, it must also have a factor smaller than `√n`.

---

### P3. Sum of All Even Numbers in a List

**📝 Problem Statement:**
Write a function to accept a list of numbers and return the sum of all even numbers in the list.

✅ **Guided Solution:**

```python
def sum_of_evens(numbers):
    total = 0
    for num in numbers:
        if num % 2 == 0:    # Check if even
            total += num
    return total

# Take input from user
nums = []
n = int(input("How many numbers? "))

for i in range(n):
    num = int(input(f"Enter number {i + 1}: "))
    nums.append(num)

result = sum_of_evens(nums)

print(f"\nList     : {nums}")
print(f"Even Sum : {result}")
```

**Output:**
```
How many numbers? 6
Enter number 1: 1
Enter number 2: 2
Enter number 3: 3
Enter number 4: 4
Enter number 5: 5
Enter number 6: 6

List     : [1, 2, 3, 4, 5, 6]
Even Sum : 12
```

---

### P4. Count Vowels and Consonants

**📝 Problem Statement:**
Write a function that takes a string as input and returns the number of vowels and consonants in it.

✅ **Guided Solution:**

```python
def count_vowels_consonants(text):
    vowels     = "aeiouAEIOU"
    vowel_count     = 0
    consonant_count = 0

    for char in text:
        if char.isalpha():              # Only count letters
            if char in vowels:
                vowel_count += 1
            else:
                consonant_count += 1

    return vowel_count, consonant_count

# Take input from user
text = input("Enter a string: ")

vowels, consonants = count_vowels_consonants(text)

print(f"\nString     : {text}")
print(f"Vowels     : {vowels}")
print(f"Consonants : {consonants}")
```

**Output:**
```
Enter a string: Hello World

String     : Hello World
Vowels     : 3
Consonants : 7
```

💡 **Key Tip:** `char.isalpha()` ensures we skip spaces, digits, and special characters — we only count actual letters.

---

### P5. Power of a Number Without Built-in

**📝 Problem Statement:**
Write a function to calculate the power of a number (x^y) without using built-in power functions.

✅ **Guided Solution:**

```python
def power(x, y):
    # Handle negative exponent
    if y < 0:
        return 1 / power(x, -y)

    result = 1
    for _ in range(y):    # Multiply x by itself y times
        result *= x

    return result

# Take input from user
x = float(input("Enter base (x)    : "))
y = int(input("Enter exponent (y) : "))

result = power(x, y)
print(f"\n{x} ^ {y} = {result}")
```

**Output:**
```
Enter base (x)    : 2
Enter exponent (y): 8

2.0 ^ 8 = 256.0
```

💡 **Key Tip:** We do NOT use `**` or `math.pow()` — instead we use a loop to multiply `x` by itself `y` times.

---

---

## 📘 Section 2: Lists

> 📋 **Source:** Assignment 3 (P1–P5) + Assignment 4 (P6–P7)

---

### P1. Largest and Smallest from 10 Numbers

**📝 Problem Statement:**
Write a program to create a list of 10 numbers and print the largest and smallest element.

✅ **Guided Solution:**

```python
numbers = []

# Take 10 numbers from user
print("Enter 10 numbers:")
for i in range(10):
    num = int(input(f"  Number {i + 1}: "))
    numbers.append(num)

# Find largest and smallest
largest  = numbers[0]
smallest = numbers[0]

for num in numbers:
    if num > largest:
        largest = num
    if num < smallest:
        smallest = num

print(f"\nList     : {numbers}")
print(f"Largest  : {largest}")
print(f"Smallest : {smallest}")
```

**Output:**
```
Enter 10 numbers:
  Number 1: 34
  Number 2: 12
  ...

List     : [34, 12, 78, 5, 90, 23, 45, 67, 11, 56]
Largest  : 90
Smallest : 5
```

💡 **Key Tip:** We do NOT use `max()` or `min()` — we manually track `largest` and `smallest` using a loop.

---

### P2. Remove Duplicates Without Using a Set

**📝 Problem Statement:**
Write a program to remove duplicate elements from a list without using a set.

✅ **Guided Solution:**

```python
numbers = [1, 2, 2, 3, 4, 4, 5, 1, 6, 3]

unique = []

for num in numbers:
    if num not in unique:    # Only add if not already present
        unique.append(num)

print(f"Original : {numbers}")
print(f"Unique   : {unique}")
```

**Output:**
```
Original : [1, 2, 2, 3, 4, 4, 5, 1, 6, 3]
Unique   : [1, 2, 3, 4, 5, 6]
```

💡 **Key Tip:** `if num not in unique` checks the already-built list — this avoids using `set()` as required.

---

### P3. Reverse a List Without reverse()

**📝 Problem Statement:**
Write a program to reverse a list without using the built-in `reverse()` method.

✅ **Guided Solution:**

```python
numbers = [10, 20, 30, 40, 50]

reversed_list = []

# Traverse from last index to first
for i in range(len(numbers) - 1, -1, -1):
    reversed_list.append(numbers[i])

print(f"Original : {numbers}")
print(f"Reversed : {reversed_list}")
```

**Output:**
```
Original : [10, 20, 30, 40, 50]
Reversed : [50, 40, 30, 20, 10]
```

💡 **Key Tip:** `range(len(numbers) - 1, -1, -1)` starts from the last index and goes backwards to 0.

---

### P4. Merge Two Lists and Sort

**📝 Problem Statement:**
Write a program to merge two lists and sort the resulting list.

✅ **Guided Solution:**

```python
list1 = [5, 3, 8, 1]
list2 = [7, 2, 9, 4, 6]

# Merge using + operator
merged = list1 + list2

# Sort using built-in sort
merged.sort()

print(f"List 1 : {list1}")
print(f"List 2 : {list2}")
print(f"Merged : {list1 + list2}")
print(f"Sorted : {merged}")
```

**Output:**
```
List 1 : [5, 3, 8, 1]
List 2 : [7, 2, 9, 4, 6]
Merged : [5, 3, 8, 1, 7, 2, 9, 4, 6]
Sorted : [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

### P5. Count Occurrences of Each Element

**📝 Problem Statement:**
Write a program to count how many times each element appears in a list.

✅ **Guided Solution:**

```python
items = ['apple', 'banana', 'apple', 'cherry',
         'banana', 'apple', 'cherry', 'mango']

count = {}

for item in items:
    if item in count:
        count[item] += 1      # Already seen → increment
    else:
        count[item] = 1       # First time → set to 1

print("Element Frequencies:")
for item, freq in count.items():
    print(f"  {item:<10} → {freq} time(s)")
```

**Output:**
```
Element Frequencies:
  apple      → 3 time(s)
  banana     → 2 time(s)
  cherry     → 2 time(s)
  mango      → 1 time(s)
```

---

### P6. Student Marks Analysis

**📝 Problem Statement:**
Create a program to store marks of 10 students in a list. Find the highest mark, lowest mark, and average mark.

✅ **Guided Solution:**

```python
marks = []

# Take marks of 10 students
print("Enter marks of 10 students:")
for i in range(10):
    mark = float(input(f"  Student {i + 1}: "))
    marks.append(mark)

# Find highest
highest = marks[0]
for m in marks:
    if m > highest:
        highest = m

# Find lowest
lowest = marks[0]
for m in marks:
    if m < lowest:
        lowest = m

# Calculate average
total   = 0
for m in marks:
    total += m
average = total / len(marks)

print(f"\nMarks   : {marks}")
print(f"Highest : {highest}")
print(f"Lowest  : {lowest}")
print(f"Average : {average:.2f}")
```

**Output:**
```
Enter marks of 10 students:
  Student 1: 78
  Student 2: 92
  ...

Marks   : [78.0, 92.0, 85.0, 60.0, 73.0, 88.0, 95.0, 55.0, 70.0, 82.0]
Highest : 95.0
Lowest  : 55.0
Average : 77.80
```

---

### P7. Shopping Cart Management

**📝 Problem Statement:**
Create a shopping cart using a list. Perform operations: Add item, Remove item, Display all items.

✅ **Guided Solution:**

```python
cart = []

def add_item(item):
    cart.append(item)
    print(f"  ✅ '{item}' added to cart.")

def remove_item(item):
    if item in cart:
        cart.remove(item)
        print(f"  🗑️  '{item}' removed from cart.")
    else:
        print(f"  ❌ '{item}' not found in cart.")

def display_cart():
    if not cart:
        print("  Cart is empty.")
    else:
        print("  🛒 Cart Items:")
        for i, item in enumerate(cart, 1):
            print(f"    {i}. {item}")
    print(f"  Total items: {len(cart)}")

# Test operations
add_item("Apple")
add_item("Milk")
add_item("Bread")
add_item("Eggs")

print()
display_cart()

print()
remove_item("Milk")
remove_item("Butter")     # Not in cart

print()
display_cart()
```

**Output:**
```
  ✅ 'Apple' added to cart.
  ✅ 'Milk' added to cart.
  ✅ 'Bread' added to cart.
  ✅ 'Eggs' added to cart.

  🛒 Cart Items:
    1. Apple
    2. Milk
    3. Bread
    4. Eggs
  Total items: 4

  🗑️  'Milk' removed from cart.
  ❌ 'Butter' not found in cart.

  🛒 Cart Items:
    1. Apple
    2. Bread
    3. Eggs
  Total items: 3
```

---

---

## 📘 Section 3: Tuples

> 📋 **Source:** Assignment 4 — Tuple Problems

---

### P1. Employee Record Using Tuple

**📝 Problem Statement:**
Store employee details (Employee ID, Name, Department, Salary) using tuples. Display all details and identify the employee with the highest salary.

✅ **Guided Solution:**

```python
# Each tuple → (Employee ID, Name, Department, Salary)
employees = [
    (101, "Alice",   "IT",      75000),
    (102, "Bob",     "HR",      55000),
    (103, "Charlie", "Finance", 90000),
    (104, "Diana",   "IT",      85000),
    (105, "Eve",     "HR",      60000),
]

# Display all employee details
print("=" * 55)
print(f"  {'ID':<6} {'Name':<12} {'Department':<12} {'Salary':>10}")
print("=" * 55)

for emp in employees:
    emp_id, name, dept, salary = emp    # Tuple unpacking
    print(f"  {emp_id:<6} {name:<12} {dept:<12} ₹{salary:>9,}")

# Find employee with highest salary
top_employee = employees[0]

for emp in employees:
    if emp[3] > top_employee[3]:    # Compare salary (index 3)
        top_employee = emp

print("=" * 55)
print(f"\n🏆 Highest Salary Employee:")
print(f"   ID         : {top_employee[0]}")
print(f"   Name       : {top_employee[1]}")
print(f"   Department : {top_employee[2]}")
print(f"   Salary     : ₹{top_employee[3]:,}")
```

**Output:**
```
=======================================================
  ID     Name         Department     Salary
=======================================================
  101    Alice        IT             ₹ 75,000
  102    Bob          HR             ₹ 55,000
  103    Charlie      Finance        ₹ 90,000
  104    Diana        IT             ₹ 85,000
  105    Eve          HR             ₹ 60,000
=======================================================

🏆 Highest Salary Employee:
   ID         : 103
   Name       : Charlie
   Department : Finance
   Salary     : ₹90,000
```

💡 **Key Tip:** `emp_id, name, dept, salary = emp` is **tuple unpacking** — assigns each element to a variable in one line.

---

### P2. Coordinate Distance Calculation

**📝 Problem Statement:**
Store multiple coordinate points in tuples. Display all points and identify the point nearest to the origin (0, 0).

✅ **Guided Solution:**

```python
import math

# Each tuple → (x, y)
points = [
    (3, 4),
    (1, 1),
    (6, 8),
    (2, 2),
    (0, 5),
    (1, 0),
]

def distance_from_origin(point):
    x, y = point
    # Distance formula: √(x² + y²)
    return math.sqrt(x**2 + y**2)

# Display all points with distances
print(f"  {'Point':<12} {'Distance from Origin':>22}")
print("  " + "-" * 36)

for point in points:
    dist = distance_from_origin(point)
    print(f"  {str(point):<12} {dist:>22.4f}")

# Find nearest point
nearest = points[0]

for point in points:
    if distance_from_origin(point) < distance_from_origin(nearest):
        nearest = point

print("\n🎯 Nearest Point to Origin:")
print(f"   Point    : {nearest}")
print(f"   Distance : {distance_from_origin(nearest):.4f}")
```

**Output:**
```
  Point        Distance from Origin
  ------------------------------------
  (3, 4)                      5.0000
  (1, 1)                      1.4142
  (6, 8)                     10.0000
  (2, 2)                      2.8284
  (0, 5)                      5.0000
  (1, 0)                      1.0000

🎯 Nearest Point to Origin:
   Point    : (1, 0)
   Distance : 1.0000
```

💡 **Key Tip:** Distance formula from origin = `√(x² + y²)`. Point `(1, 0)` has the shortest distance of `1.0`.

---

---

## 📘 Section 4: Dictionaries

> 📋 **Source:** Assignment 4 — Dictionary Problems

---

### P1. Student Information System

**📝 Problem Statement:**
Create a dictionary — Key: Student ID, Value: Student Name. Perform: Add student, Update student, Delete student, Display all records.

✅ **Guided Solution:**

```python
students = {}

def add_student(student_id, name):
    if student_id in students:
        print(f"  ⚠️  ID {student_id} already exists.")
    else:
        students[student_id] = name
        print(f"  ✅ Student '{name}' added (ID: {student_id})")

def update_student(student_id, new_name):
    if student_id in students:
        old_name = students[student_id]
        students[student_id] = new_name
        print(f"  ✅ Updated: '{old_name}' → '{new_name}'")
    else:
        print(f"  ❌ Student ID {student_id} not found.")

def delete_student(student_id):
    if student_id in students:
        name = students.pop(student_id)
        print(f"  🗑️  Student '{name}' (ID: {student_id}) deleted.")
    else:
        print(f"  ❌ Student ID {student_id} not found.")

def display_all():
    if not students:
        print("  No records found.")
    else:
        print(f"\n  {'ID':<6} {'Name':<20}")
        print("  " + "-" * 28)
        for sid, name in students.items():
            print(f"  {sid:<6} {name:<20}")
        print(f"  Total students: {len(students)}")

# Test
add_student(101, "Alice")
add_student(102, "Bob")
add_student(103, "Charlie")
add_student(101, "Duplicate")     # Duplicate ID

display_all()

print()
update_student(102, "Robert")
delete_student(103)
delete_student(999)               # Non-existent

display_all()
```

**Output:**
```
  ✅ Student 'Alice' added (ID: 101)
  ✅ Student 'Bob' added (ID: 102)
  ✅ Student 'Charlie' added (ID: 103)
  ⚠️  ID 101 already exists.

  ID     Name
  ----------------------------
  101    Alice
  102    Bob
  103    Charlie
  Total students: 3

  ✅ Updated: 'Bob' → 'Robert'
  🗑️  Student 'Charlie' (ID: 103) deleted.
  ❌ Student ID 999 not found.

  ID     Name
  ----------------------------
  101    Alice
  102    Robert
  Total students: 2
```

---

### P2. Product Inventory Management

**📝 Problem Statement:**
Create a dictionary — Key: Product Name, Value: Quantity. Perform: Add product, Update stock, Display low stock products.

✅ **Guided Solution:**

```python
inventory = {}

LOW_STOCK_LIMIT = 5    # Threshold for low stock alert

def add_product(name, quantity):
    if name in inventory:
        print(f"  ⚠️  '{name}' already exists. Use update.")
    else:
        inventory[name] = quantity
        print(f"  ✅ '{name}' added — Qty: {quantity}")

def update_stock(name, quantity):
    if name in inventory:
        old_qty = inventory[name]
        inventory[name] = quantity
        print(f"  ✅ '{name}' stock updated: {old_qty} → {quantity}")
    else:
        print(f"  ❌ Product '{name}' not found.")

def display_low_stock():
    low = {k: v for k, v in inventory.items() if v <= LOW_STOCK_LIMIT}
    if not low:
        print("  ✅ No low stock items.")
    else:
        print(f"\n  ⚠️  LOW STOCK ALERT (≤ {LOW_STOCK_LIMIT} units):")
        print(f"  {'Product':<20} {'Qty':>5}")
        print("  " + "-" * 28)
        for name, qty in low.items():
            print(f"  {name:<20} {qty:>5}")

def display_all():
    print(f"\n  {'Product':<20} {'Qty':>8}")
    print("  " + "-" * 30)
    for name, qty in inventory.items():
        status = " ⚠️ LOW" if qty <= LOW_STOCK_LIMIT else ""
        print(f"  {name:<20} {qty:>8}{status}")

# Test
add_product("Apples",   50)
add_product("Bananas",  3)
add_product("Milk",     12)
add_product("Bread",    4)
add_product("Eggs",     24)
add_product("Butter",   2)

display_all()

print()
update_stock("Milk",  2)
update_stock("Eggs",  30)
update_stock("Sugar", 10)    # Not found

display_low_stock()
```

**Output:**
```
  ✅ 'Apples' added — Qty: 50
  ✅ 'Bananas' added — Qty: 3
  ✅ 'Milk' added — Qty: 12
  ✅ 'Bread' added — Qty: 4
  ✅ 'Eggs' added — Qty: 24
  ✅ 'Butter' added — Qty: 2

  Product               Qty
  ------------------------------
  Apples                  50
  Bananas                  3 ⚠️ LOW
  Milk                    12
  Bread                    4 ⚠️ LOW
  Eggs                    24
  Butter                   2 ⚠️ LOW

  ✅ 'Milk' stock updated: 12 → 2
  ✅ 'Eggs' stock updated: 24 → 30
  ❌ Product 'Sugar' not found.

  ⚠️  LOW STOCK ALERT (≤ 5 units):
  Product               Qty
  ----------------------------
  Bananas                  3
  Bread                    4
  Butter                   2
  Milk                     2
```

---

---

## 📘 Section 5: Sets

> 📋 **Source:** Assignment 4 — Set Problem

---

### P1. Common Subjects Finder

**📝 Problem Statement:**
Two students have selected subjects stored in sets. Find common subjects, unique subjects for each, and all subjects without duplication.

✅ **Guided Solution:**

```python
# Subjects selected by each student
student_a = {"Python", "Linux", "Networks", "Security", "Databases"}
student_b = {"Java",   "Linux", "Networks", "Cloud",    "Python"}

# Common subjects (intersection)
common = student_a & student_b

# Unique to Student A only
only_a = student_a - student_b

# Unique to Student B only
only_b = student_b - student_a

# All subjects combined (union — no duplicates)
all_subjects = student_a | student_b

# Display results
print("📚 Student A Subjects:", student_a)
print("📚 Student B Subjects:", student_b)

print(f"\n✅ Common Subjects        : {common}")
print(f"🔵 Unique to Student A   : {only_a}")
print(f"🟡 Unique to Student B   : {only_b}")
print(f"📋 All Subjects (no dup) : {all_subjects}")
print(f"\nTotal Unique Subjects    : {len(all_subjects)}")
```

**Output:**
```
📚 Student A Subjects: {'Python', 'Linux', 'Networks', 'Security', 'Databases'}
📚 Student B Subjects: {'Java', 'Linux', 'Networks', 'Cloud', 'Python'}

✅ Common Subjects        : {'Python', 'Linux', 'Networks'}
🔵 Unique to Student A   : {'Security', 'Databases'}
🟡 Unique to Student B   : {'Java', 'Cloud'}
📋 All Subjects (no dup) : {'Python', 'Linux', 'Networks', 'Security',
                             'Databases', 'Java', 'Cloud'}

Total Unique Subjects    : 7
```

💡 **Key Tip:**
- `&` → Intersection (common)
- `-` → Difference (unique to one side)
- `|` → Union (all, no duplicates)

---

---

## 📘 Section 6: Strings

> ⚠️ **Note:** Strings were not covered in Assignments 3 or 4.
> These programs are added at **faculty assignment difficulty level** to complete the topic coverage.

---

### P1. Count Words, Characters, and Spaces

**📝 Problem Statement:**
Write a program that takes a string as input and counts the number of words, total characters, and spaces.

✅ **Guided Solution:**

```python
text = input("Enter a string: ")

# Count characters (including spaces)
total_chars = len(text)

# Count spaces
spaces = text.count(' ')

# Count words
words = text.split()
word_count = len(words)

# Count characters without spaces
chars_no_space = len(text.replace(' ', ''))

print(f"\nString          : '{text}'")
print(f"Total Characters: {total_chars}")
print(f"Characters      : {chars_no_space} (excluding spaces)")
print(f"Spaces          : {spaces}")
print(f"Words           : {word_count}")
```

**Output:**
```
Enter a string: Hello World from Python

String          : 'Hello World from Python'
Total Characters: 23
Characters      : 20 (excluding spaces)
Spaces          : 3
Words           : 4
```

---

### P2. Check if String is a Palindrome

**📝 Problem Statement:**
Write a program to check whether a given string is a palindrome or not (ignore case and spaces).

✅ **Guided Solution:**

```python
def is_palindrome(text):
    # Remove spaces and convert to lowercase
    cleaned = text.replace(' ', '').lower()

    # Compare string with its reverse
    reversed_text = cleaned[::-1]

    return cleaned == reversed_text

# Take input from user
text = input("Enter a string: ")

if is_palindrome(text):
    print(f"'{text}' is a Palindrome ✅")
else:
    print(f"'{text}' is NOT a Palindrome ❌")
```

**Output:**
```
Enter a string: Racecar
'Racecar' is a Palindrome ✅

Enter a string: Hello
'Hello' is NOT a Palindrome ❌

Enter a string: A man a plan a canal Panama
'A man a plan a canal Panama' is a Palindrome ✅
```

💡 **Key Tip:** `cleaned[::-1]` reverses a string — `step = -1` means go backwards from end to start.

---

### P3. Find the Most Frequent Character

**📝 Problem Statement:**
Write a program to find the most frequently occurring character in a string (ignore spaces).

✅ **Guided Solution:**

```python
text = input("Enter a string: ")

# Remove spaces and convert to lowercase
cleaned = text.replace(' ', '').lower()

# Build frequency dictionary manually
freq = {}
for char in cleaned:
    if char in freq:
        freq[char] += 1
    else:
        freq[char] = 1

# Find most frequent character
max_char  = None
max_count = 0

for char, count in freq.items():
    if count > max_count:
        max_count = count
        max_char  = char

print(f"\nString             : '{text}'")
print(f"Character Frequency: {freq}")
print(f"Most Frequent      : '{max_char}' → {max_count} times")
```

**Output:**
```
Enter a string: programming

String             : 'programming'
Character Frequency: {'p': 1, 'r': 2, 'o': 1, 'g': 2, 'a': 1, 'm': 2, 'i': 1, 'n': 1}
Most Frequent      : 'r' → 2 times
```

---

### P4. Reverse Each Word in a Sentence

**📝 Problem Statement:**
Write a program to reverse each individual word in a sentence while keeping the word order the same.

✅ **Guided Solution:**

```python
sentence = input("Enter a sentence: ")

# Split sentence into words
words = sentence.split()

# Reverse each word individually
reversed_words = []
for word in words:
    reversed_word = word[::-1]    # Reverse individual word
    reversed_words.append(reversed_word)

# Join back into a sentence
result = ' '.join(reversed_words)

print(f"\nOriginal : '{sentence}'")
print(f"Reversed : '{result}'")
```

**Output:**
```
Enter a sentence: Hello World Python

Original : 'Hello World Python'
Reversed : 'olleH dlroW nohtyP'
```

💡 **Key Tip:** We reverse each **word** — NOT the whole sentence. Word order stays the same, only letters inside each word are reversed.

---

---

## 🏛️ Section 7: Classes & Objects (OOP)

> ⚠️ **Note:** OOP was not covered in Assignments 3 or 4.
> These programs are added at **faculty assignment difficulty level** to complete the topic coverage.

---

### P1. Student Class with Marks and Grade

**📝 Problem Statement:**
Create a `Student` class that stores a student's name and marks. Add a method to calculate the grade based on marks and display the result.

✅ **Guided Solution:**

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def get_grade(self):
        if self.marks >= 90:
            return 'A+'
        elif self.marks >= 80:
            return 'A'
        elif self.marks >= 70:
            return 'B'
        elif self.marks >= 60:
            return 'C'
        elif self.marks >= 40:
            return 'D'
        else:
            return 'F'

    def display(self):
        grade  = self.get_grade()
        result = "PASS" if grade != 'F' else "FAIL"
        print(f"  Name  : {self.name}")
        print(f"  Marks : {self.marks}")
        print(f"  Grade : {grade}")
        print(f"  Result: {result}")
        print()

# Create student objects
s1 = Student("Alice",   92)
s2 = Student("Bob",     73)
s3 = Student("Charlie", 35)

s1.display()
s2.display()
s3.display()
```

**Output:**
```
  Name  : Alice
  Marks : 92
  Grade : A+
  Result: PASS

  Name  : Bob
  Marks : 73
  Grade : B
  Result: PASS

  Name  : Charlie
  Marks : 35
  Grade : F
  Result: FAIL
```

💡 **Key Tip:**
- `__init__` is the **constructor** — called automatically when `Student(...)` is used
- `self` refers to the **current object** — it connects the method to the instance

---

### P2. BankAccount Class with Deposit and Withdraw

**📝 Problem Statement:**
Create a `BankAccount` class that stores account holder name and balance. Add methods to deposit, withdraw, and display balance.

✅ **Guided Solution:**

```python
class BankAccount:
    def __init__(self, holder, balance=0):
        self.holder  = holder
        self.balance = balance

    def deposit(self, amount):
        if amount <= 0:
            print("  ❌ Deposit amount must be positive.")
        else:
            self.balance += amount
            print(f"  ✅ Deposited ₹{amount} | Balance: ₹{self.balance}")

    def withdraw(self, amount):
        if amount <= 0:
            print("  ❌ Withdrawal amount must be positive.")
        elif amount > self.balance:
            print(f"  ❌ Insufficient funds! Balance: ₹{self.balance}")
        else:
            self.balance -= amount
            print(f"  ✅ Withdrew ₹{amount} | Balance: ₹{self.balance}")

    def display(self):
        print(f"  Account Holder : {self.holder}")
        print(f"  Balance        : ₹{self.balance}")

# Test
acc = BankAccount("Alice", 1000)

print("── Initial ──")
acc.display()

print("\n── Transactions ──")
acc.deposit(500)
acc.withdraw(200)
acc.withdraw(2000)    # Insufficient
acc.deposit(-100)     # Invalid

print("\n── Final ──")
acc.display()
```

**Output:**
```
── Initial ──
  Account Holder : Alice
  Balance        : ₹1000

── Transactions ──
  ✅ Deposited ₹500 | Balance: ₹1500
  ✅ Withdrew ₹200 | Balance: ₹1300
  ❌ Insufficient funds! Balance: ₹1300
  ❌ Deposit amount must be positive.

── Final ──
  Account Holder : Alice
  Balance        : ₹1300
```

---

### P3. Animal → Dog Inheritance

**📝 Problem Statement:**
Create an `Animal` base class with a `speak()` method. Create a `Dog` class that inherits from `Animal` and overrides the `speak()` method. Demonstrate inheritance and method overriding.

✅ **Guided Solution:**

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

    def eat(self):
        return f"{self.name} is eating."


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)     # Call Animal's __init__
        self.breed = breed

    def speak(self):               # Override parent method
        return f"{self.name} says: Woof! 🐕"

    def fetch(self):
        return f"{self.name} fetched the ball!"


class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name)
        self.color = color

    def speak(self):               # Override parent method
        return f"{self.name} says: Meow! 🐈"


# Test
dog = Dog("Rex", "Labrador")
cat = Cat("Whiskers", "Orange")

print("── Dog ──────────────────────")
print(f"  Name  : {dog.name}")
print(f"  Breed : {dog.breed}")
print(f"  {dog.speak()}")
print(f"  {dog.eat()}")
print(f"  {dog.fetch()}")

print("\n── Cat ──────────────────────")
print(f"  Name  : {cat.name}")
print(f"  Color : {cat.color}")
print(f"  {cat.speak()}")
print(f"  {cat.eat()}")

# Inheritance check
print("\n── Inheritance Check ────────")
print(f"  Dog is Animal? {isinstance(dog, Animal)}")
print(f"  Cat is Animal? {isinstance(cat, Animal)}")
print(f"  Dog is Cat?    {isinstance(dog, Cat)}")
```

**Output:**
```
── Dog ──────────────────────
  Name  : Rex
  Breed : Labrador
  Rex says: Woof! 🐕
  Rex is eating.
  Rex fetched the ball!

── Cat ──────────────────────
  Name  : Whiskers
  Color : Orange
  Whiskers says: Meow! 🐈
  Whiskers is eating.

── Inheritance Check ────────
  Dog is Animal? True
  Cat is Animal? True
  Dog is Cat?    False
```

💡 **Key Tip:** `super().__init__(name)` calls the **parent class constructor** — this way we don't have to rewrite `self.name = name` in every child class.

---

### P4. Shape → Rectangle and Circle with Area

**📝 Problem Statement:**
Create a `Shape` base class. Create `Rectangle` and `Circle` child classes that inherit from `Shape` and implement their own `area()` and `perimeter()` methods.

✅ **Guided Solution:**

```python
import math

class Shape:
    def __init__(self, name):
        self.name = name

    def area(self):
        return 0

    def perimeter(self):
        return 0

    def display(self):
        print(f"  Shape     : {self.name}")
        print(f"  Area      : {self.area():.2f}")
        print(f"  Perimeter : {self.perimeter():.2f}")
        print()


class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__("Rectangle")
        self.width  = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)


class Circle(Shape):
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius

    def area(self):
        return math.pi * self.radius ** 2

    def perimeter(self):               # Circumference
        return 2 * math.pi * self.radius


# Test
r = Rectangle(5, 10)
c = Circle(7)

r.display()
c.display()
```

**Output:**
```
  Shape     : Rectangle
  Area      : 50.00
  Perimeter : 30.00

  Shape     : Circle
  Area      : 153.94
  Perimeter : 43.98
```

💡 **Key Tip:** This is **polymorphism** — both `Rectangle` and `Circle` have `area()` and `perimeter()` methods, but each gives a **different result** based on the shape's own formula.

---

---

## 🌐 Section 8: Sockets

> 📋 **Source:** Faculty Class Programs — 3 Levels

---

### 🐛 Bug Analysis Summary

| Program | Line | ❌ Bug | ✅ Fix |
|---|---|---|---|
| **Client 1** | `client_socket.connect("localhost", 8888)` | `connect()` takes a **single tuple** argument | `connect(("localhost", 8888))` |
| **Server 1** | After `bind()` → directly `accept()` | Missing `listen()` call between `bind()` and `accept()` | Add `server_socket.listen(1)` before `accept()` |

---

### Level 1 — Basic One-Way Message (With Bug Fix)

**📝 Faculty's Original Code (With Bugs):**

```python
# ── ORIGINAL CLIENT 1 (BUGGY) ──────────────────
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client_socket.connect("localhost", 8888)   # ❌ BUG: Should be a tuple

client_socket.send("Hello from client".encode())
client_socket.close()
```

```python
# ── ORIGINAL SERVER 1 (BUGGY) ──────────────────
import socket

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server_socket.bind(("localhost", 8888))
print("server is waiting for connection")

# ❌ BUG: Missing server_socket.listen(1)

client_socket, add = server_socket.accept()

print("connected to", add)

message = client_socket.recv(1024)
print("received message from client", message)

client_socket.close()
server_socket.close()
```

---

**🐛 Bug Breakdown:**

**Bug 1 — Client:**
```python
# ❌ WRONG — Two separate arguments
client_socket.connect("localhost", 8888)

# ✅ CORRECT — Single tuple argument
client_socket.connect(("localhost", 8888))
```
> `connect()` takes exactly **one argument** — a tuple of `(host, port)`.
> Passing them separately raises: `TypeError: connect() takes exactly one argument`

**Bug 2 — Server:**
```python
# ❌ WRONG — Missing listen() before accept()
server_socket.bind(("localhost", 8888))
client_socket, add = server_socket.accept()

# ✅ CORRECT — listen() must come between bind() and accept()
server_socket.bind(("localhost", 8888))
server_socket.listen(1)                 # ← This was missing
client_socket, add = server_socket.accept()
```
> Without `listen()`, the socket is not in a listening state.
> Calling `accept()` directly raises: `OSError: [Errno 22] Invalid argument`

---

✅ **Fixed Code:**

```python
# ══ FILE: server_level1.py (FIXED) ═══════════════
import socket

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server_socket.bind(("localhost", 8888))

server_socket.listen(1)                 # ✅ FIX: Added listen()
print("Server is waiting for connection...")

client_socket, addr = server_socket.accept()
print("Connected to:", addr)

message = client_socket.recv(1024)
print("Received message from client:", message.decode())

client_socket.close()
server_socket.close()
```

```python
# ══ FILE: client_level1.py (FIXED) ═══════════════
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client_socket.connect(("localhost", 8888))  # ✅ FIX: Wrapped in tuple

client_socket.send("Hello from client".encode())
print("Message sent to server.")

client_socket.close()
```

**Server Output:**
```
Server is waiting for connection...
Connected to: ('127.0.0.1', 54231)
Received message from client: Hello from client
```

**Client Output:**
```
Message sent to server.
```

---

### Level 2 — Two-Way Message Exchange

**📝 Faculty's Original Code:**
> ✅ No bugs — faculty code is correct. Solution presented as-is with comments added.

```python
# ══ FILE: server_level2.py ═══════════════════════
import socket

# Step 1: Create socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Step 2: Bind IP and port
server_socket.bind(("localhost", 5000))

# Step 3: Listen for connection
server_socket.listen(1)
print("Server waiting for connection...")

# Step 4: Accept client connection
client_socket, addr = server_socket.accept()
print("Connected with:", addr)

# Step 5: Receive message from client
client_message = client_socket.recv(1024).decode()
print("Message from Client:", client_message)

# Step 6: Send reply to client
server_message = input("Enter message for Client: ")
client_socket.send(server_message.encode())

# Step 7: Close connections
client_socket.close()
server_socket.close()
```

```python
# ══ FILE: client_level2.py ═══════════════════════
import socket

# Step 1: Create socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Step 2: Connect to server
client_socket.connect(("localhost", 5000))

# Step 3: Send message to server
message = input("Enter message for Server: ")
client_socket.send(message.encode())

# Step 4: Receive reply from server
server_reply = client_socket.recv(1024).decode()
print("Message from Server:", server_reply)

# Step 5: Close socket
client_socket.close()
```

**Terminal Flow:**
```
── Client Terminal ──────────────────────────────────
Enter message for Server: Hello Server!
Message from Server: Hello Client, got your message!

── Server Terminal ──────────────────────────────────
Server waiting for connection...
Connected with: ('127.0.0.1', 54300)
Message from Client: Hello Server!
Enter message for Client: Hello Client, got your message!
```

---

### Level 3 — Multi-Message Chat Loop

**📝 Faculty's Original Code:**
> ✅ No bugs — faculty code is correct. Solution presented as-is with comments added.

```python
# ══ FILE: server_level3.py ═══════════════════════
import socket

# Create and configure socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("localhost", 5000))
server_socket.listen(1)
print("Server waiting for connection...")

# Accept client
client_socket, address = server_socket.accept()
print("Connected with:", address)

while True:
    # Receive message from client
    client_msg = client_socket.recv(1024).decode()

    # If client sends 'bye', exit loop
    if client_msg.lower() == "bye":
        print("Client disconnected.")
        break

    print("Client:", client_msg)

    # Send reply to client
    server_msg = input("Server: ")
    client_socket.send(server_msg.encode())

    # If server sends 'bye', exit loop
    if server_msg.lower() == "bye":
        break

# Close sockets
client_socket.close()
server_socket.close()
```

```python
# ══ FILE: client_level3.py ═══════════════════════
import socket

# Create socket and connect
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(("localhost", 5000))
print("Connected to server.")

while True:
    # Send message to server
    msg = input("Client: ")
    client_socket.send(msg.encode())

    # If client sends 'bye', exit loop
    if msg.lower() == "bye":
        break

    # Receive reply from server
    server_reply = client_socket.recv(1024).decode()
    print("Server:", server_reply)

    # If server sends 'bye', exit loop
    if server_reply.lower() == "bye":
        break

# Close socket
client_socket.close()
```

**Sample Chat Output:**
```
── Client Terminal ──────────────────────────────────
Connected to server.
Client: Hello!
Server: Hi there!
Client: How are you?
Server: I'm good. You?
Client: bye

── Server Terminal ──────────────────────────────────
Server waiting for connection...
Connected with: ('127.0.0.1', 54350)
Client: Hello!
Server: Hi there!
Client: How are you?
Server: I'm good. You?
Client disconnected.
```

💡 **Key Tip — Socket Flow Summary:**
```
SERVER FLOW                      CLIENT FLOW
────────────────────────────     ────────────────────────────
socket()  → Create socket        socket()  → Create socket
bind()    → Set IP + Port        connect() → Connect to server
listen()  → Start listening      send()    → Send data
accept()  → Wait for client      recv()    → Receive data
recv()    → Get client data      close()   → Done
send()    → Reply to client
close()   → Done
```

---

---

## 📊 Part 4 Summary

| Section | Source | Programs |
|---|---|---|
| ⚙️ Functions | Assignment 3 | 5 |
| 📘 Lists | Assignment 3 + 4 | 7 |
| 📘 Tuples | Assignment 4 | 2 |
| 📘 Dictionaries | Assignment 4 | 2 |
| 📘 Sets | Assignment 4 | 1 |
| 📘 Strings | Added — Faculty Level | 4 |
| 🏛️ Classes & OOP | Added — Faculty Level | 4 |
| 🌐 Sockets | Faculty Class Programs | 3 |
| | **GRAND TOTAL** | **28 Programs** |

---

## 🐛 Socket Bug Fix Quick Reference

| Bug | Wrong | Fixed |
|---|---|---|
| `connect()` args | `connect("localhost", 8888)` | `connect(("localhost", 8888))` |
| Missing `listen()` | `bind()` → `accept()` | `bind()` → `listen(1)` → `accept()` |

---

> 💡 **Final Exam Tips:**
>
> **Functions:**
> - Always check for edge cases — negative numbers, empty lists
> - Recursive functions need a **base case** to stop
>
> **Data Structures:**
> - `List` → ordered, mutable, allows duplicates
> - `Tuple` → ordered, immutable, use for fixed data
> - `Dict` → key-value pairs, keys must be unique
> - `Set` → unordered, unique elements, use `&` `|` `-`
>
> **OOP:**
> - `__init__` = constructor | `self` = current object
> - `super().__init__()` = call parent constructor
> - Child class can **override** parent methods
>
> **Sockets — Most Common Bugs:**
> - `connect()` needs a **tuple** → `connect(("host", port))`
> - Server needs `listen()` **before** `accept()`
> - Always **encode** before send → `.encode()`
> - Always **decode** after recv → `.decode()`

---

## 🏁 Complete Series — All Parts

| Part | File | Topics | Programs/Questions |
|---|---|---|---|
| **Part 1** | `Part1_DataStructures.md` | Dict, List, Tuple, Set, String | 75 Questions |
| **Part 2** | `Part2_Functions.md` | Functions, Lambda, Regex | 45 Questions |
| **Part 3** | `Part3_OOP_Sockets.md` | OOP, Sockets | 30 Questions |
| **Part 4** | `Part4_FacultyAssignments.md` | All Topics (Assignment Based) | 28 Programs |
| | | **GRAND TOTAL** | **178** |

---

*📁 Part of: Python-Exam-Prep Series | PGCP-ITISS | February 2026*
*⬅️ Previous: [Part 3 — OOP & Sockets](Part3_OOP_Sockets.md)*
*🏠 Index: [README.md](README.md)*