# 🐍 Python Exam Prep — Part 2: Functions, Lambda/Map/Filter & Regular Expressions

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Topics](https://img.shields.io/badge/Topics-3-green)
![Questions](https://img.shields.io/badge/Questions-45-orange)
![Level](https://img.shields.io/badge/Level-Basic%20to%20Medium-yellow)

---

## 📌 Index

| # | Topic | Questions |
|---|---|---|
| 6 | [⚙️ Functions](#️-topic-6-functions) | Q1–Q15 |
| 7 | [⚙️ Lambda / Map / Filter](#️-topic-7-lambda--map--filter) | Q1–Q15 |
| 8 | [🔎 Regular Expressions](#-topic-8-regular-expressions) | Q1–Q15 |

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

## ⚙️ Topic 6: Functions

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `def func():` | Define a function |
| `def func(a, b):` | Function with parameters |
| `return value` | Return a value |
| `def func(a=10):` | Default argument |
| `def func(*args):` | Variable positional arguments |
| `def func(**kwargs):` | Variable keyword arguments |
| `func()` | Call a function |
| `help(func)` | View docstring |
| `"""docstring"""` | Document a function |
| `global x` | Access global variable inside function |
| `lambda x: x+1` | Anonymous one-liner function |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a function in Python? Why do we use functions?**

✅ **Answer:**
- A function is a **reusable block of code** that performs a specific task.
- Defined using the `def` keyword.
- Functions help in:
  - **Code reusability** — write once, use many times
  - **Modularity** — break large problems into smaller pieces
  - **Readability** — makes code easier to understand
  - **Maintainability** — easier to fix and update

```python
# Without function — repeated code
print("Hello Alice")
print("Hello Bob")

# With function — reusable
def greet(name):
    print(f"Hello {name}")

greet("Alice")
greet("Bob")
```

💡 **Key Tip:** A function that doesn't have a `return` statement returns `None` by default.

---

**Q2. What is the output?**

```python
def add(a, b=10):
    return a + b

print(add(5))
print(add(5, 20))
print(add(b=3, a=7))

def info(*args, **kwargs):
    print("args:  ", args)
    print("kwargs:", kwargs)

info(1, 2, 3, name="Alice", age=25)
```

✅ **Answer:**
```
15
25
10
args:   (1, 2, 3)
kwargs: {'name': 'Alice', 'age': 25}
```

💡 **Key Tip:**
- `*args` collects extra **positional** arguments as a **tuple**
- `**kwargs` collects extra **keyword** arguments as a **dictionary**

---

**Q3. True or False — with reason.**

```
a) A function can return multiple values.
b) Default arguments must come before non-default arguments.
c) *args collects keyword arguments.
d) A function must always have a return statement.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Multiple return values | ✅ True | Python returns them as a **tuple** — `return a, b` |
| b) Default args before non-default | ❌ False | **Non-default** must come first — `def f(a, b=10)` ✅ |
| c) `*args` = keyword args | ❌ False | `*args` = **positional**; `**kwargs` = keyword |
| d) `return` is mandatory | ❌ False | Without `return`, function returns `None` automatically |

---

**Q4. Fill in the blank.**

```python
# Define a function that takes a name and age
# and prints "Hello <name>, you are <age> years old."
def greet(______, ______):
    print(f"Hello {______}, you are {______} years old.")

# Call with positional arguments
greet(______, ______)

# Call with keyword arguments
greet(______ = "Bob", ______ = 30)

# Define a function that returns the square of a number
def square(n):
    return ______

print(square(5))
```

✅ **Answer:**
```python
def greet(name, age):
    print(f"Hello {name}, you are {age} years old.")

greet("Alice", 25)
greet(name="Bob", age=30)

def square(n):
    return n * n

print(square(5))
```

**Output:**
```
Hello Alice, you are 25 years old.
Hello Bob, you are 30 years old.
25
```

---

**Q5. What is the output?**

```python
def outer(x):
    def inner(y):
        return x + y
    return inner

add5 = outer(5)
print(add5(3))
print(add5(10))

def multiply(a, b):
    """Returns the product of a and b."""
    return a * b

print(multiply(4, 5))
print(multiply.__doc__)
```

✅ **Answer:**
```
8
15
20
Returns the product of a and b.
```

💡 **Key Tip:**
- `outer()` returns the `inner` function — this is called a **closure**
- `.__doc__` accesses the **docstring** of a function

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a function that takes two numbers and returns the greater one.**

✅ **Solution:**
```python
def greater(a, b):
    if a > b:
        return a
    else:
        return b

# Test
print(greater(10, 20))   # 20
print(greater(55, 33))   # 55
print(greater(7, 7))     # 7 (equal)
```

**Output:**
```
20
55
7
```

---

**Q7. Write a function that checks if a number is even or odd.**

✅ **Solution:**
```python
def check_even_odd(n):
    if n % 2 == 0:
        return "Even"
    else:
        return "Odd"

# Test multiple numbers
numbers = [1, 2, 7, 10, 33, 100]

for num in numbers:
    print(f"  {num} → {check_even_odd(num)}")
```

**Output:**
```
  1 → Odd
  2 → Even
  7 → Odd
  10 → Even
  33 → Odd
  100 → Even
```

---

**Q8. Write a function using `*args` to calculate the sum of any number of values.**

✅ **Solution:**
```python
def total_sum(*args):
    result = 0
    for num in args:
        result += num
    return result

# Test with different number of arguments
print(total_sum(1, 2))             # 3
print(total_sum(10, 20, 30))       # 60
print(total_sum(5, 5, 5, 5, 5))   # 25
print(total_sum())                 # 0
```

**Output:**
```
3
60
25
0
```

💡 **Key Tip:** `*args` lets you pass **any number** of positional arguments — they arrive as a tuple.

---

**Q9. Write a function using `**kwargs` to display a person's profile.**

✅ **Solution:**
```python
def display_profile(**kwargs):
    print("--- Profile ---")
    for key, value in kwargs.items():
        print(f"  {key.capitalize()}: {value}")
    print()

# Test with different fields
display_profile(name="Alice", age=25, city="Pune")
display_profile(name="Bob", age=30, city="Mumbai", job="Engineer")
```

**Output:**
```
--- Profile ---
  Name: Alice
  Age: 25
  City: Pune

--- Profile ---
  Name: Bob
  Age: 30
  City: Mumbai
  Job: Engineer
```

---

**Q10. Write a function that returns multiple values — the quotient and remainder of two numbers.**

✅ **Solution:**
```python
def divide(a, b):
    if b == 0:
        return None, None  # Handle division by zero
    quotient  = a // b
    remainder = a % b
    return quotient, remainder

# Unpack returned values
q, r = divide(17, 5)
print(f"17 ÷ 5 → Quotient: {q}, Remainder: {r}")

q, r = divide(20, 4)
print(f"20 ÷ 4 → Quotient: {q}, Remainder: {r}")
```

**Output:**
```
17 ÷ 5 → Quotient: 3, Remainder: 2
20 ÷ 4 → Quotient: 5, Remainder: 0
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a recursive function to calculate the factorial of a number.**

✅ **Solution:**
```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

# Test
for i in range(6):
    print(f"  {i}! = {factorial(i)}")
```

**Output:**
```
  0! = 1
  1! = 1
  2! = 2
  3! = 6
  4! = 24
  5! = 120
```

💡 **Step-by-step for `factorial(4)`:**
```
factorial(4)
→ 4 * factorial(3)
→ 4 * 3 * factorial(2)
→ 4 * 3 * 2 * factorial(1)
→ 4 * 3 * 2 * 1
→ 24
```

---

**Q12. Write a function that accepts a list of numbers and returns a dictionary with their sum, average, min, and max.**

✅ **Solution:**
```python
def analyze(numbers):
    if not numbers:
        return None

    result = {
        'count'  : len(numbers),
        'sum'    : sum(numbers),
        'average': sum(numbers) / len(numbers),
        'min'    : min(numbers),
        'max'    : max(numbers)
    }
    return result

# Test
nums = [23, 45, 12, 67, 34, 89, 10]
stats = analyze(nums)

print("Numbers:", nums)
print()
for key, value in stats.items():
    print(f"  {key.capitalize():10}: {value}")
```

**Output:**
```
Numbers: [23, 45, 12, 67, 34, 89, 10]

  Count     : 7
  Sum       : 280
  Average   : 40.0
  Min       : 10
  Max       : 89
```

---

**Q13. Write a function that takes a string and returns a dictionary of character frequencies.**

✅ **Solution:**
```python
def char_frequency(text):
    freq = {}
    for char in text:
        if char != ' ':                    # Skip spaces
            freq[char] = freq.get(char, 0) + 1
    return freq

def display_frequency(text):
    freq  = char_frequency(text.lower())
    # Sort by frequency descending
    sorted_freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)

    print(f"Text: '{text}'")
    print("Character Frequencies:")
    for char, count in sorted_freq:
        bar = '█' * count
        print(f"  '{char}': {count:2}  {bar}")

display_frequency("Hello World")
```

**Output:**
```
Text: 'Hello World'
Character Frequencies:
  'l': 3  ███
  'o': 2  ██
  'h': 1  █
  'e': 1  █
  'w': 1  █
  'r': 1  █
  'd': 1  █
```

---

**Q14. Write a function with a default argument that greets a user. If no name given, greet as "Guest".**

✅ **Solution:**
```python
def greet(name="Guest", greeting="Hello"):
    return f"{greeting}, {name}! Welcome."

# Test all combinations
print(greet())                          # Both defaults
print(greet("Alice"))                   # Custom name
print(greet("Bob", "Hi"))              # Both custom
print(greet(greeting="Hey"))           # Only greeting overridden
print(greet(name="Diana", greeting="Good Morning"))
```

**Output:**
```
Hello, Guest! Welcome.
Hello, Alice! Welcome.
Hi, Bob! Welcome.
Hey, Guest! Welcome.
Good Morning, Diana! Welcome.
```

---

**Q15. Write a program using nested functions — outer function multiplies, inner function adds.**

✅ **Solution:**
```python
def calculator(multiply_by):
    """Outer function — sets the multiplier"""

    def add_then_multiply(a, b):
        """Inner function — adds a and b, then multiplies by outer value"""
        total = a + b
        result = total * multiply_by
        print(f"  ({a} + {b}) × {multiply_by} = {result}")
        return result

    return add_then_multiply   # Return the inner function

# Create specialized calculators
double = calculator(2)
triple = calculator(3)

print("Using double (×2):")
double(3, 4)    # (3+4) × 2 = 14
double(5, 5)    # (5+5) × 2 = 20

print("\nUsing triple (×3):")
triple(3, 4)    # (3+4) × 3 = 21
triple(2, 8)    # (2+8) × 3 = 30
```

**Output:**
```
Using double (×2):
  (3 + 4) × 2 = 14
  (5 + 5) × 2 = 20

Using triple (×3):
  (3 + 4) × 3 = 21
  (2 + 8) × 3 = 30
```

💡 **Key Tip:** This is a **closure** — `add_then_multiply` "remembers" the `multiply_by` value from the outer scope even after `calculator()` has finished executing.

---

---

## ⚙️ Topic 7: Lambda / Map / Filter

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `lambda x: x+1` | Lambda with one argument |
| `lambda x, y: x+y` | Lambda with two arguments |
| `lambda x: x if x>0 else 0` | Lambda with condition |
| `map(func, iterable)` | Apply func to every element |
| `list(map(...))` | Convert map result to list |
| `filter(func, iterable)` | Keep elements where func is True |
| `list(filter(...))` | Convert filter result to list |
| `sorted(l, key=lambda x: x)` | Sort using lambda as key |
| `max(l, key=lambda x: x)` | Max using lambda as key |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Lambda function? How is it different from a regular function?**

✅ **Answer:**
- A lambda is an **anonymous (nameless), one-line function**.
- Defined using the `lambda` keyword.
- Can take **any number of arguments** but only **one expression**.
- Used when a short, throwaway function is needed.

| Feature | `def` Function | `lambda` Function |
|---|---|---|
| Name | Has a name | Anonymous |
| Lines | Multiple lines | Single expression |
| Return | Explicit `return` | Implicit return |
| Docstring | ✅ Supported | ❌ Not supported |
| Use Case | Complex logic | Quick, short operations |

```python
# Regular function
def square(x):
    return x * x

# Lambda equivalent
square = lambda x: x * x

print(square(5))   # 25
```

---

**Q2. What is the output?**

```python
double  = lambda x: x * 2
add     = lambda x, y: x + y
is_even = lambda x: x % 2 == 0

print(double(7))
print(add(3, 4))
print(is_even(10))
print(is_even(7))

nums = [1, 2, 3, 4, 5]
result = list(map(lambda x: x ** 2, nums))
print(result)
```

✅ **Answer:**
```
14
7
True
False
[1, 4, 9, 16, 25]
```

---

**Q3. True or False — with reason.**

```
a) Lambda functions can contain multiple expressions.
b) map() returns a list directly.
c) filter() keeps elements where the function returns True.
d) Lambda functions can be used as arguments to other functions.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) Multiple expressions | ❌ False | Lambda allows only **one expression** |
| b) `map()` returns list | ❌ False | Returns a **map object** — wrap with `list()` |
| c) `filter()` keeps True items | ✅ True | That's exactly what filter does |
| d) Lambda as argument | ✅ True | Commonly used with `map()`, `filter()`, `sorted()` |

---

**Q4. Fill in the blank.**

```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Use map to triple every number
tripled = list(map(lambda x: ______, nums))
print("Tripled:", tripled)

# Use filter to keep only odd numbers
odds = list(filter(lambda x: ______, nums))
print("Odds:", odds)

# Sort a list of strings by length
words = ['banana', 'fig', 'apple', 'kiwi']
sorted_words = sorted(words, key=lambda x: ______)
print("By length:", sorted_words)
```

✅ **Answer:**
```python
tripled     = list(map(lambda x: x * 3, nums))
odds        = list(filter(lambda x: x % 2 != 0, nums))
sorted_words = sorted(words, key=lambda x: len(x))
```

**Output:**
```
Tripled: [3, 6, 9, 12, 15, 18, 21, 24, 27, 30]
Odds: [1, 3, 5, 7, 9]
By length: ['fig', 'kiwi', 'apple', 'banana']
```

---

**Q5. What is the output?**

```python
data = [('Alice', 88), ('Bob', 72), ('Charlie', 95), ('Diana', 80)]

# Sort by score ascending
asc = sorted(data, key=lambda x: x[1])
print("Ascending: ", asc)

# Sort by score descending
desc = sorted(data, key=lambda x: x[1], reverse=True)
print("Descending:", desc)

# Get only names using map
names = list(map(lambda x: x[0], data))
print("Names:", names)

# Filter students with score > 80
passed = list(filter(lambda x: x[1] > 80, data))
print("Passed:", passed)
```

✅ **Answer:**
```
Ascending:  [('Bob', 72), ('Diana', 80), ('Alice', 88), ('Charlie', 95)]
Descending: [('Charlie', 95), ('Alice', 88), ('Diana', 80), ('Bob', 72)]
Names: ['Alice', 'Bob', 'Charlie', 'Diana']
Passed: [('Alice', 88), ('Charlie', 95)]
```

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a program using `map()` to convert a list of temperatures from Celsius to Fahrenheit.**

✅ **Solution:**
```python
celsius = [0, 20, 37, 100, -10]

# Formula: F = (C × 9/5) + 32
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))

print("Celsius:    ", celsius)
print("Fahrenheit: ", fahrenheit)
```

**Output:**
```
Celsius:     [0, 20, 37, 100, -10]
Fahrenheit:  [32.0, 68.0, 98.6, 212.0, 14.0]
```

---

**Q7. Write a program using `filter()` to extract all positive numbers from a list.**

✅ **Solution:**
```python
numbers = [10, -3, 0, 7, -15, 22, -1, 5, -8]

positives = list(filter(lambda x: x > 0, numbers))
negatives = list(filter(lambda x: x < 0, numbers))
zeros     = list(filter(lambda x: x == 0, numbers))

print("Original:  ", numbers)
print("Positives: ", positives)
print("Negatives: ", negatives)
print("Zeros:     ", zeros)
```

**Output:**
```
Original:   [10, -3, 0, 7, -15, 22, -1, 5, -8]
Positives:  [10, 7, 22, 5]
Negatives:  [-3, -15, -1, -8]
Zeros:      [0]
```

---

**Q8. Write a program using `map()` to convert all strings in a list to uppercase.**

✅ **Solution:**
```python
cities = ['pune', 'mumbai', 'delhi', 'bangalore', 'chennai']

upper_cities = list(map(lambda x: x.upper(), cities))
title_cities = list(map(lambda x: x.title(), cities))

print("Original: ", cities)
print("Upper:    ", upper_cities)
print("Title:    ", title_cities)
```

**Output:**
```
Original:  ['pune', 'mumbai', 'delhi', 'bangalore', 'chennai']
Upper:     ['PUNE', 'MUMBAI', 'DELHI', 'BANGALORE', 'CHENNAI']
Title:     ['Pune', 'Mumbai', 'Delhi', 'Bangalore', 'Chennai']
```

---

**Q9. Write a program using `filter()` to keep only strings that start with a vowel.**

✅ **Solution:**
```python
words  = ['apple', 'banana', 'orange', 'grape', 'umbrella', 'cherry', 'ice']
vowels = 'aeiouAEIOU'

starts_with_vowel = list(filter(lambda w: w[0] in vowels, words))

print("All words:          ", words)
print("Starts with vowel:  ", starts_with_vowel)
```

**Output:**
```
All words:           ['apple', 'banana', 'orange', 'grape', 'umbrella', 'cherry', 'ice']
Starts with vowel:   ['apple', 'orange', 'umbrella', 'ice']
```

---

**Q10. Write a program using `map()` and `filter()` together — square all even numbers from a list.**

✅ **Solution:**
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Step 1: Filter even numbers
evens = filter(lambda x: x % 2 == 0, nums)

# Step 2: Square the even numbers
squared_evens = list(map(lambda x: x ** 2, evens))

print("Original:            ", nums)
print("Squared Even Numbers:", squared_evens)
```

**Output:**
```
Original:             [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Squared Even Numbers: [4, 16, 36, 64, 100]
```

💡 **Key Tip:** You can **chain** `filter()` and `map()` — filter first, then transform.

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program using `map()` to apply a discount of 10% to all prices in a list and round to 2 decimal places.**

✅ **Solution:**
```python
prices = [199.99, 450.00, 89.50, 1200.00, 34.75]

# Apply 10% discount
discounted = list(map(lambda p: round(p * 0.90, 2), prices))

print("Original Prices:    ", prices)
print("After 10% Discount: ", discounted)
print()

# Display with formatting
print(f"{'Item':<6} {'Original':>10} {'Discounted':>12} {'Saved':>8}")
print("-" * 40)

for i, (orig, disc) in enumerate(zip(prices, discounted), 1):
    saved = round(orig - disc, 2)
    print(f"  {i:<6} ₹{orig:>9.2f}  ₹{disc:>10.2f}  ₹{saved:>6.2f}")
```

**Output:**
```
Original Prices:     [199.99, 450.0, 89.5, 1200.0, 34.75]
After 10% Discount:  [179.99, 405.0, 80.55, 1080.0, 31.27]

Item    Original  Discounted    Saved
----------------------------------------
  1      ₹199.99      ₹179.99   ₹20.00
  2      ₹450.00      ₹405.00   ₹45.00
  3       ₹89.50       ₹80.55    ₹8.95
  4     ₹1200.00     ₹1080.00  ₹120.00
  5       ₹34.75       ₹31.27    ₹3.48
```

---

**Q12. Write a program using `filter()` to find all students who passed (marks ≥ 40) and failed.**

✅ **Solution:**
```python
students = [
    ('Alice',   72),
    ('Bob',     35),
    ('Charlie', 88),
    ('Diana',   40),
    ('Eve',     28),
    ('Frank',   55),
    ('Grace',   15),
]

passed = list(filter(lambda s: s[1] >= 40, students))
failed = list(filter(lambda s: s[1] < 40,  students))

print("=" * 30)
print("     RESULT CARD")
print("=" * 30)

print("\n✅ PASSED:")
for name, marks in passed:
    print(f"   {name:<10} → {marks}")

print("\n❌ FAILED:")
for name, marks in failed:
    print(f"   {name:<10} → {marks}")

print(f"\nTotal: {len(students)} | Passed: {len(passed)} | Failed: {len(failed)}")
```

**Output:**
```
==============================
     RESULT CARD
==============================

✅ PASSED:
   Alice      → 72
   Charlie    → 88
   Diana      → 40
   Frank      → 55

❌ FAILED:
   Bob        → 35
   Eve        → 28
   Grace      → 15

Total: 7 | Passed: 4 | Failed: 3
```

---

**Q13. Write a program using `sorted()` with lambda to sort a list of dictionaries by a specific key.**

✅ **Solution:**
```python
employees = [
    {'name': 'Alice',   'dept': 'IT',      'salary': 75000},
    {'name': 'Bob',     'dept': 'HR',      'salary': 55000},
    {'name': 'Charlie', 'dept': 'IT',      'salary': 90000},
    {'name': 'Diana',   'dept': 'Finance', 'salary': 65000},
    {'name': 'Eve',     'dept': 'HR',      'salary': 60000},
]

# Sort by salary ascending
by_salary = sorted(employees, key=lambda e: e['salary'])

# Sort by name alphabetically
by_name = sorted(employees, key=lambda e: e['name'])

print("Sorted by Salary:")
for emp in by_salary:
    print(f"  {emp['name']:<10} | {emp['dept']:<8} | ₹{emp['salary']:,}")

print("\nSorted by Name:")
for emp in by_name:
    print(f"  {emp['name']:<10} | {emp['dept']:<8} | ₹{emp['salary']:,}")
```

**Output:**
```
Sorted by Salary:
  Bob        | HR       | ₹55,000
  Eve        | HR       | ₹60,000
  Diana      | Finance  | ₹65,000
  Alice      | IT       | ₹75,000
  Charlie    | IT       | ₹90,000

Sorted by Name:
  Alice      | IT       | ₹75,000
  Bob        | HR       | ₹55,000
  Charlie    | IT       | ₹90,000
  Diana      | Finance  | ₹65,000
  Eve        | HR       | ₹60,000
```

---

**Q14. Write a program using `map()` and `filter()` together to process a list of names — keep names longer than 4 characters and convert them to uppercase.**

✅ **Solution:**
```python
names = ['Al', 'Alice', 'Bob', 'Charlie', 'Eve', 'Diana', 'Tom', 'Frank']

# Step 1: Filter names longer than 4 characters
long_names = filter(lambda n: len(n) > 4, names)

# Step 2: Map to uppercase
result = list(map(lambda n: n.upper(), long_names))

print("All Names:       ", names)
print("Filtered + Upper:", result)

# ── Alternative: one-liner ──────────────────────────
one_liner = list(map(lambda n: n.upper(),
                     filter(lambda n: len(n) > 4, names)))
print("One-liner:       ", one_liner)
```

**Output:**
```
All Names:        ['Al', 'Alice', 'Bob', 'Charlie', 'Eve', 'Diana', 'Tom', 'Frank']
Filtered + Upper: ['ALICE', 'CHARLIE', 'DIANA', 'FRANK']
One-liner:        ['ALICE', 'CHARLIE', 'DIANA', 'FRANK']
```

---

**Q15. Write a program using lambda with `map()` to compute the area of circles from a list of radii.**

✅ **Solution:**
```python
import math

radii = [1, 2, 3, 5, 7, 10]

# Compute area: π × r²
areas = list(map(lambda r: round(math.pi * r ** 2, 2), radii))

# Compute circumference: 2 × π × r
circumferences = list(map(lambda r: round(2 * math.pi * r, 2), radii))

print(f"{'Radius':>8} | {'Area':>12} | {'Circumference':>15}")
print("-" * 42)

for r, a, c in zip(radii, areas, circumferences):
    print(f"{r:>8} | {a:>12} | {c:>15}")
```

**Output:**
```
  Radius |         Area |   Circumference
------------------------------------------
       1 |         3.14 |            6.28
       2 |        12.57 |           12.57
       3 |        28.27 |           18.85
       5 |        78.54 |           31.42
       7 |       153.94 |           43.98
      10 |       314.16 |           62.83
```

---

---

## 🔎 Topic 8: Regular Expressions

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `import re` | Import regex module |
| `re.match(p, s)` | Match at the **beginning** of string |
| `re.search(p, s)` | Search **anywhere** in string |
| `re.findall(p, s)` | Find **all** matches → returns list |
| `re.sub(p, r, s)` | **Substitute** pattern with replacement |
| `re.split(p, s)` | **Split** string by pattern |
| `.` | Any character except newline |
| `\d` | Any digit `[0-9]` |
| `\D` | Any non-digit |
| `\w` | Any word character `[a-zA-Z0-9_]` |
| `\W` | Any non-word character |
| `\s` | Any whitespace |
| `\S` | Any non-whitespace |
| `^` | Start of string |
| `$` | End of string |
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 |
| `{n}` | Exactly n times |
| `{n,m}` | Between n and m times |
| `[abc]` | Character class — a, b, or c |
| `[^abc]` | Not a, b, or c |
| `(abc)` | Group |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Regular Expression? What module do we use in Python?**

✅ **Answer:**
- A **Regular Expression (regex)** is a sequence of characters that defines a **search pattern**.
- Used for: **searching**, **matching**, **replacing**, and **splitting** strings.
- Python uses the built-in **`re` module**.

```python
import re

text = "My phone is 9876543210"

# Search for a 10-digit phone number
match = re.search(r'\d{10}', text)

if match:
    print("Found:", match.group())   # 9876543210
```

💡 **Key Tip:** Always use **raw strings** `r"..."` for regex patterns to avoid issues with backslashes.

---

**Q2. What is the output?**

```python
import re

text = "Hello World 123 Python 456"

# findall digits
digits = re.findall(r'\d+', text)
print("Digits:", digits)

# findall words
words = re.findall(r'\w+', text)
print("Words:", words)

# search for 'World'
match = re.search(r'World', text)
print("Found at index:", match.start())

# sub - replace digits with #
result = re.sub(r'\d', '#', text)
print("Replaced:", result)
```

✅ **Answer:**
```
Digits: ['123', '456']
Words: ['Hello', 'World', '123', 'Python', '456']
Found at index: 6
Replaced: Hello World ### Python ###
```

---

**Q3. What does each pattern match? Match the pattern to its meaning.**

```
Pattern    →   Meaning
─────────────────────────────────
\d+        →   ?
\w+        →   ?
\s         →   ?
\S+        →   ?
^Hello     →   ?
world$     →   ?
[aeiou]    →   ?
[^0-9]     →   ?
```

✅ **Answer:**

| Pattern | Meaning |
|---|---|
| `\d+` | One or more **digits** |
| `\w+` | One or more **word characters** (letters, digits, underscore) |
| `\s` | A single **whitespace** character (space, tab, newline) |
| `\S+` | One or more **non-whitespace** characters |
| `^Hello` | String that **starts with** "Hello" |
| `world$` | String that **ends with** "world" |
| `[aeiou]` | Any single **vowel** |
| `[^0-9]` | Any character that is **not a digit** |

---

**Q4. Fill in the blank.**

```python
import re

text = "Contact us at support@example.com or admin@test.org"

# Find all email addresses
emails = re.______(r'[\w.]+@[\w]+\.\w+', text)
print("Emails:", emails)

# Replace all emails with [REDACTED]
cleaned = re.______(r'[\w.]+@[\w]+\.\w+', '[REDACTED]', text)
print("Cleaned:", cleaned)

# Split text by whitespace
tokens = re.______(r'\s+', text)
print("Tokens:", tokens)
```

✅ **Answer:**
```python
emails  = re.findall(r'[\w.]+@[\w]+\.\w+', text)
cleaned = re.sub(r'[\w.]+@[\w]+\.\w+', '[REDACTED]', text)
tokens  = re.split(r'\s+', text)
```

**Output:**
```
Emails: ['support@example.com', 'admin@test.org']
Cleaned: Contact us at [REDACTED] or [REDACTED]
Tokens: ['Contact', 'us', 'at', 'support@example.com', 'or', 'admin@test.org']
```

---

**Q5. What is the difference between `re.match()` and `re.search()`?**

✅ **Answer:**

| Feature | `re.match()` | `re.search()` |
|---|---|---|
| Where it looks | Only at the **beginning** | **Anywhere** in the string |
| Returns | Match object or `None` | Match object or `None` |

```python
import re

text = "Hello World"

m1 = re.match(r'World', text)
m2 = re.search(r'World', text)

print("match:", m1)    # None — 'World' not at start
print("search:", m2)   # Match — 'World' found at index 6
```

**Output:**
```
match: None
search: <re.Match object; span=(6, 11), match='World'>
```

💡 **Key Tip:** When in doubt, use `re.search()` — it's more flexible.

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Write a program to check if a string contains only digits using regex.**

✅ **Solution:**
```python
import re

def is_all_digits(s):
    pattern = r'^\d+$'
    if re.match(pattern, s):
        return "✅ All digits"
    else:
        return "❌ Not all digits"

test_cases = ["12345", "123abc", "000", "98.6", ""]

for case in test_cases:
    print(f"  '{case}' → {is_all_digits(case)}")
```

**Output:**
```
  '12345' → ✅ All digits
  '123abc' → ❌ Not all digits
  '000' → ✅ All digits
  '98.6' → ❌ Not all digits
  '' → ❌ Not all digits
```

---

**Q7. Write a program to extract all phone numbers from a text using `re.findall()`.**

✅ **Solution:**
```python
import re

text = """
Contact Details:
  Alice: 9876543210
  Bob:   +91-9123456789
  Support: 022-27654321
  Helpline: 1800-123-4567
"""

# Match 10-digit numbers (with optional separators)
pattern = r'\d[\d\-]{8,}\d'

phones = re.findall(pattern, text)

print("Extracted Phone Numbers:")
for phone in phones:
    print(f"  {phone}")
```

**Output:**
```
Extracted Phone Numbers:
  9876543210
  91-9123456789
  022-27654321
  1800-123-4567
```

---

**Q8. Write a program to replace all whitespace sequences in a string with a single space using `re.sub()`.**

✅ **Solution:**
```python
import re

text = "Hello   World!    This    is    Python."

# Replace multiple spaces/tabs with single space
cleaned = re.sub(r'\s+', ' ', text).strip()

print("Original:", repr(text))
print("Cleaned: ", repr(cleaned))
```

**Output:**
```
Original: 'Hello   World!    This    is    Python.'
Cleaned:  'Hello World! This is Python.'
```

💡 **Key Tip:** `\s+` matches **one or more** whitespace characters (spaces, tabs, newlines).

---

**Q9. Write a program to split a sentence into words using `re.split()`, handling multiple spaces and punctuation.**

✅ **Solution:**
```python
import re

sentences = [
    "Hello, World! How are you?",
    "Python...is   awesome!!!",
    "one  two   three    four"
]

for sentence in sentences:
    # Split on non-word characters (spaces, punctuation)
    words = re.split(r'\W+', sentence)
    # Remove empty strings from result
    words = [w for w in words if w]
    print(f"Input:  '{sentence}'")
    print(f"Words:  {words}")
    print()
```

**Output:**
```
Input:  'Hello, World! How are you?'
Words:  ['Hello', 'World', 'How', 'are', 'you']

Input:  'Python...is   awesome!!!'
Words:  ['Python', 'is', 'awesome']

Input:  'one  two   three    four'
Words:  ['one', 'two', 'three', 'four']
```

---

**Q10. Write a program to find all words that start with a capital letter using regex.**

✅ **Solution:**
```python
import re

text = "Alice went to London. She met Bob and Charlie near the Thames River."

# Find words starting with uppercase
pattern = r'\b[A-Z][a-z]*\b'
capitals = re.findall(pattern, text)

print("Text:          ", text)
print("Capital Words: ", capitals)
```

**Output:**
```
Text:           Alice went to London. She met Bob and Charlie near the Thames River.
Capital Words:  ['Alice', 'London', 'She', 'Bob', 'Charlie', 'Thames', 'River']
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a program to validate an email address using regex.**

✅ **Solution:**
```python
import re

def validate_email(email):
    # Pattern: word chars/dots before @, word chars after @, dot + 2-4 chars at end
    pattern = r'^[\w\.-]+@[\w\.-]+\.[a-zA-Z]{2,4}$'

    if re.match(pattern, email):
        return "✅ Valid"
    else:
        return "❌ Invalid"

test_emails = [
    "user@example.com",
    "user.name@domain.org",
    "invalid-email",
    "missing@dotcom",
    "@nodomain.com",
    "user@.com",
    "valid123@test.in"
]

print(f"{'Email':<30} | {'Status'}")
print("-" * 45)

for email in test_emails:
    print(f"  {email:<28} | {validate_email(email)}")
```

**Output:**
```
Email                          | Status
---------------------------------------------
  user@example.com             | ✅ Valid
  user.name@domain.org         | ✅ Valid
  invalid-email                | ❌ Invalid
  missing@dotcom               | ❌ Invalid
  @nodomain.com                | ❌ Invalid
  user@.com                    | ❌ Invalid
  valid123@test.in             | ✅ Valid
```

---

**Q12. Write a program to remove leading zeros from an IP address using `re.sub()`.**

✅ **Solution:**
```python
import re

def clean_ip(ip):
    # Match leading zeros in each octet
    # Replace one or more zeros followed by a digit
    cleaned = re.sub(r'\b0+(\d)', r'\1', ip)
    return cleaned

test_ips = [
    "216.08.094.196",
    "001.002.003.004",
    "192.168.001.010",
    "010.000.000.001",
    "255.255.255.000"
]

print(f"{'Original IP':<22} → {'Cleaned IP'}")
print("-" * 45)

for ip in test_ips:
    print(f"  {ip:<20} → {clean_ip(ip)}")
```

**Output:**
```
Original IP            → Cleaned IP
---------------------------------------------
  216.08.094.196       → 216.8.94.196
  001.002.003.004      → 1.2.3.4
  192.168.001.010      → 192.168.1.10
  010.000.000.001      → 10.0.0.1
  255.255.255.000      → 255.255.255.0
```

---

**Q13. Write a program to convert a CamelCase string to snake_case using `re.sub()`.**

✅ **Solution:**
```python
import re

def camel_to_snake(name):
    # Step 1: Insert underscore before each uppercase letter (except the first)
    step1 = re.sub(r'([A-Z])', r'_\1', name)
    # Step 2: Convert entire string to lowercase
    step2 = step1.lower()
    # Step 3: Remove leading underscore if present
    result = step2.lstrip('_')
    return result

test_cases = [
    "thisIsAConversionExample",
    "CamelCaseString",
    "myVariableName",
    "HTMLParser",
    "simpleword"
]

print(f"{'CamelCase':<30} → {'snake_case'}")
print("-" * 55)

for name in test_cases:
    print(f"  {name:<28} → {camel_to_snake(name)}")
```

**Output:**
```
CamelCase                      → snake_case
-------------------------------------------------------
  thisIsAConversionExample     → this_is_a_conversion_example
  CamelCaseString              → camel_case_string
  myVariableName               → my_variable_name
  HTMLParser                   → h_t_m_l_parser
  simpleword                   → simpleword
```

---

**Q14. Write a program to parse a log file line using `re.split()` and extract timestamp, level, message, and details.**

✅ **Solution:**
```python
import re

def parse_log(log_line):
    # Pattern: split on ']- ', '- ', ': '
    # First extract timestamp from brackets
    pattern = r'[\[\]\-:]\s*'

    # Better approach: use specific delimiters
    # Format: [TIMESTAMP]- LEVEL- MESSAGE: DETAILS

    # Extract timestamp (between first [ and ])
    ts_match = re.search(r'\[(.+?)\]', log_line)
    timestamp = ts_match.group(1) if ts_match else None

    # Remove timestamp and leading bracket/dash
    remaining = re.sub(r'^\[.+?\]-\s*', '', log_line)

    # Split remaining by '- ' pattern
    parts = re.split(r'\s*-\s*', remaining, maxsplit=2)

    # Handle colon separator in message:details
    if len(parts) == 2 and ':' in parts[1]:
        msg_parts = parts[1].split(':', 1)
        parts = [parts[0], msg_parts[0].strip(), msg_parts[1].strip()]

    return {
        'timestamp': timestamp,
        'level'    : parts[0].strip() if len(parts) > 0 else None,
        'message'  : parts[1].strip() if len(parts) > 1 else None,
        'details'  : parts[2].strip() if len(parts) > 2 else None
    }

# Test
logs = [
    "[2025-12-17 10:00:00]- ERROR- User login failed: Invalid credentials",
    "[2025-12-17 10:05:23]- INFO- Server started: Port 8080",
    "[2025-12-17 10:10:45]- WARNING- High memory usage: 92% utilized"
]

for log in logs:
    result = parse_log(log)
    print("Raw Log  :", log)
    print("Parsed   :")
    for key, val in result.items():
        print(f"   {key:<12}: {val}")
    print()
```

**Output:**
```
Raw Log  : [2025-12-17 10:00:00]- ERROR- User login failed: Invalid credentials
Parsed   :
   timestamp   : 2025-12-17 10:00:00
   level       : ERROR
   message     : User login failed
   details     : Invalid credentials

Raw Log  : [2025-12-17 10:05:23]- INFO- Server started: Port 8080
Parsed   :
   timestamp   : 2025-12-17 10:05:23
   level       : INFO
   message     : Server started
   details     : Port 8080

Raw Log  : [2025-12-17 10:10:45]- WARNING- High memory usage: 92% utilized
Parsed   :
   timestamp   : 2025-12-17 10:10:45
   level       : WARNING
   message     : High memory usage
   details     : 92% utilized
```

---

**Q15. Write a program to validate a password using regex — it must have at least 8 characters, one uppercase, one lowercase, one digit, and one special character.**

✅ **Solution:**
```python
import re

def validate_password(password):
    errors = []

    # Check each rule
    if len(password) < 8:
        errors.append("❌ Must be at least 8 characters")

    if not re.search(r'[A-Z]', password):
        errors.append("❌ Must contain at least one UPPERCASE letter")

    if not re.search(r'[a-z]', password):
        errors.append("❌ Must contain at least one lowercase letter")

    if not re.search(r'\d', password):
        errors.append("❌ Must contain at least one digit (0-9)")

    if not re.search(r'[!@#$%^&*(),.?":{}|<>]', password):
        errors.append("❌ Must contain at least one special character")

    if not errors:
        return "✅ Strong Password!"
    else:
        return "\n".join(errors)

# Test
passwords = [
    "abc",
    "password",
    "Password1",
    "P@ssw0rd",
    "Str0ng!Pass"
]

for pwd in passwords:
    print(f"Password: '{pwd}'")
    print(f"Result:   {validate_password(pwd)}")
    print()
```

**Output:**
```
Password: 'abc'
Result:   ❌ Must be at least 8 characters
          ❌ Must contain at least one UPPERCASE letter
          ❌ Must contain at least one digit (0-9)
          ❌ Must contain at least one special character

Password: 'password'
Result:   ❌ Must contain at least one UPPERCASE letter
          ❌ Must contain at least one digit (0-9)
          ❌ Must contain at least one special character

Password: 'Password1'
Result:   ❌ Must contain at least one special character

Password: 'P@ssw0rd'
Result:   ✅ Strong Password!

Password: 'Str0ng!Pass'
Result:   ✅ Strong Password!
```

---

---

## 📊 Part 2 Summary

| Topic | Q1–Q5 | Q6–Q10 | Q11–Q15 | Total |
|---|---|---|---|---|
| ⚙️ Functions | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| ⚙️ Lambda/Map/Filter | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 🔎 Regular Expressions | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| | | | **TOTAL** | **45 Questions** |

---

> 💡 **Exam Tips:**
>
> **Functions:**
> - `*args` → tuple of positional args &nbsp;|&nbsp; `**kwargs` → dict of keyword args
> - Default arguments must come **after** non-default arguments
> - A function without `return` gives back `None`
>
> **Lambda/Map/Filter:**
> - `lambda` is a **one-liner anonymous function**
> - `map()` → **transforms** every element
> - `filter()` → **keeps** elements where condition is `True`
> - Both return **iterables** — wrap with `list()` to see results
>
> **Regular Expressions:**
> - Always use **raw strings** `r"..."` for patterns
> - `re.search()` > `re.match()` for general use
> - `\d` = digit &nbsp;|&nbsp; `\w` = word char &nbsp;|&nbsp; `\s` = whitespace
> - `+` = one or more &nbsp;|&nbsp; `*` = zero or more &nbsp;|&nbsp; `?` = zero or one

---

*📁 Part of: Python-Exam-Prep Series | PGCP-ITISS | February 2026*
*⬅️ Previous: [Part 1 — Data Structures](Part1_DataStructures.md)*
*➡️ Next: [Part 3 — OOP & Sockets](Part3_OOP_Sockets.md)*