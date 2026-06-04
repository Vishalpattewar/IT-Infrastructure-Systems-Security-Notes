# 🐍 Python Exam Prep — Part 3: OOP & Sockets

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat&logo=python)
![Topics](https://img.shields.io/badge/Topics-2-green)
![Questions](https://img.shields.io/badge/Questions-30-orange)
![Level](https://img.shields.io/badge/Level-Basic%20to%20Medium-yellow)

---

## 📌 Index

| # | Topic | Questions |
|---|---|---|
| 9 | [🏛️ Classes & Objects (OOP)](#️-topic-9-classes--objects-oop) | Q1–Q15 |
| 10 | [🌐 Sockets](#-topic-10-sockets) | Q1–Q15 |

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

## 🏛️ Topic 9: Classes & Objects (OOP)

### 📋 Quick Reference

| Syntax | Description |
|---|---|
| `class MyClass:` | Define a class |
| `def __init__(self):` | Constructor — runs on object creation |
| `self.attr = value` | Instance attribute |
| `obj = MyClass()` | Create an object (instance) |
| `obj.attr` | Access instance attribute |
| `obj.method()` | Call instance method |
| `class Child(Parent):` | Inheritance |
| `super().__init__()` | Call parent constructor |
| `def __str__(self):` | String representation of object |
| `@classmethod` | Method bound to the class |
| `@staticmethod` | Method not bound to class or instance |
| `__private` | Name mangling — private attribute |
| `_protected` | Convention — protected attribute |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Class and an Object in Python? Explain with a real-world analogy.**

✅ **Answer:**

| Term | Definition | Real-World Analogy |
|---|---|---|
| **Class** | A **blueprint/template** for creating objects | Blueprint of a house |
| **Object** | An **instance** of a class with actual values | An actual house built from the blueprint |
| **Attribute** | Data/variables inside a class | Rooms, color, size of the house |
| **Method** | Functions inside a class | Actions like opening a door, turning on lights |

```python
# Class = Blueprint
class Car:
    def __init__(self, brand, color):
        self.brand = brand     # Attribute
        self.color = color     # Attribute

    def start(self):           # Method
        print(f"{self.brand} is starting...")

# Object = Actual car built from blueprint
car1 = Car("Toyota", "Red")
car2 = Car("Honda",  "Blue")

car1.start()   # Toyota is starting...
car2.start()   # Honda is starting...
```

💡 **Key Tip:** Every method inside a class must have `self` as the **first parameter** — it refers to the current object.

---

**Q2. What is the output?**

```python
class Student:
    school = "ABC Academy"      # Class attribute

    def __init__(self, name, grade):
        self.name  = name       # Instance attribute
        self.grade = grade      # Instance attribute

    def display(self):
        print(f"Name: {self.name} | Grade: {self.grade} | School: {self.school}")

s1 = Student("Alice", "A")
s2 = Student("Bob",   "B")

s1.display()
s2.display()

print(Student.school)
print(s1.name)

s1.name = "Alicia"
print(s1.name)
print(s2.name)
```

✅ **Answer:**
```
Name: Alice | Grade: A | School: ABC Academy
Name: Bob   | Grade: B | School: ABC Academy
ABC Academy
Alice
Alicia
Bob
```

💡 **Key Tip:**
- **Class attributes** are shared across all objects → `Student.school`
- **Instance attributes** belong to individual objects → `self.name`
- Changing `s1.name` does **NOT** affect `s2.name`

---

**Q3. True or False — with reason.**

```
a) __init__ is called automatically when an object is created.
b) self is a reserved keyword in Python.
c) A child class can override a parent class method.
d) A class can inherit from multiple parent classes in Python.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) `__init__` auto-called | ✅ True | It is the **constructor** — called on `ClassName()` |
| b) `self` is reserved | ❌ False | `self` is a **convention**, not a keyword — you could use any name |
| c) Child can override parent | ✅ True | This is called **method overriding** |
| d) Multiple inheritance | ✅ True | Python supports it — `class C(A, B):` |

---

**Q4. Fill in the blank.**

```python
class Rectangle:
    def __init__(self, ______, ______):
        self.width  = width
        self.height = height

    def area(self):
        return ______ * ______

    def perimeter(self):
        return 2 * (______ + ______)

    def ______(self):
        return f"Rectangle({self.width} × {self.height})"

# Create object
rect = ______(5, 10)

print(rect.area())
print(rect.perimeter())
print(rect)           # Uses __str__
```

✅ **Answer:**
```python
class Rectangle:
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

    def __str__(self):
        return f"Rectangle({self.width} × {self.height})"

rect = Rectangle(5, 10)

print(rect.area())       # 50
print(rect.perimeter())  # 30
print(rect)              # Rectangle(5 × 10)
```

---

**Q5. What is the output? — Inheritance**

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

class Dog(Animal):
    def speak(self):
        return f"{self.name} says: Woof!"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says: Meow!"

class Duck(Animal):
    pass    # No override — uses parent method

animals = [Dog("Rex"), Cat("Whiskers"), Duck("Donald"), Animal("Unknown")]

for animal in animals:
    print(animal.speak())

print(isinstance(animals[0], Dog))
print(isinstance(animals[0], Animal))
print(issubclass(Dog, Animal))
```

✅ **Answer:**
```
Rex says: Woof!
Whiskers says: Meow!
Donald makes a sound.
Unknown makes a sound.
True
True
True
```

💡 **Key Tip:**
- `Duck` has no `speak()` → it **inherits** from `Animal`
- `isinstance(obj, Class)` → checks if obj is an instance of Class
- `issubclass(Child, Parent)` → checks inheritance relationship

---

### 🔵 Q6–Q10: Basic Programs

---

**Q6. Create a `BankAccount` class with deposit and withdraw methods.**

✅ **Solution:**
```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner   = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        print(f"  ✅ Deposited ₹{amount} | Balance: ₹{self.balance}")

    def withdraw(self, amount):
        if amount > self.balance:
            print(f"  ❌ Insufficient funds! Balance: ₹{self.balance}")
        else:
            self.balance -= amount
            print(f"  ✅ Withdrew ₹{amount} | Balance: ₹{self.balance}")

    def __str__(self):
        return f"Account[{self.owner}] → ₹{self.balance}"


# Test
acc = BankAccount("Alice", 1000)
print(acc)

acc.deposit(500)
acc.withdraw(200)
acc.withdraw(2000)

print(acc)
```

**Output:**
```
Account[Alice] → ₹1000
  ✅ Deposited ₹500 | Balance: ₹1500
  ✅ Withdrew ₹200 | Balance: ₹1300
  ❌ Insufficient funds! Balance: ₹1300
Account[Alice] → ₹1300
```

---

**Q7. Create a `Circle` class that calculates area and circumference.**

✅ **Solution:**
```python
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return round(math.pi * self.radius ** 2, 2)

    def circumference(self):
        return round(2 * math.pi * self.radius, 2)

    def __str__(self):
        return (f"Circle(r={self.radius}) → "
                f"Area: {self.area()} | "
                f"Circumference: {self.circumference()}")

# Test
radii = [1, 5, 7, 10]

for r in radii:
    c = Circle(r)
    print(c)
```

**Output:**
```
Circle(r=1)  → Area: 3.14  | Circumference: 6.28
Circle(r=5)  → Area: 78.54 | Circumference: 31.42
Circle(r=7)  → Area: 153.94| Circumference: 43.98
Circle(r=10) → Area: 314.16| Circumference: 62.83
```

---

**Q8. Create a `Person` class and a `Student` class that inherits from it.**

✅ **Solution:**
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age  = age

    def introduce(self):
        return f"Hi! I'm {self.name}, {self.age} years old."

class Student(Person):
    def __init__(self, name, age, student_id, course):
        super().__init__(name, age)         # Call parent constructor
        self.student_id = student_id
        self.course     = course

    def introduce(self):                    # Override parent method
        base = super().introduce()          # Reuse parent method
        return f"{base} | ID: {self.student_id} | Course: {self.course}"

# Test
person  = Person("Alice", 30)
student = Student("Bob", 20, "S101", "Python Programming")

print(person.introduce())
print(student.introduce())

# Check inheritance
print(f"\nIs Student a Person? {issubclass(Student, Person)}")
print(f"Is Bob a Student?    {isinstance(student, Student)}")
print(f"Is Bob a Person?     {isinstance(student, Person)}")
```

**Output:**
```
Hi! I'm Alice, 30 years old.
Hi! I'm Bob, 20 years old. | ID: S101 | Course: Python Programming

Is Student a Person? True
Is Bob a Student?    True
Is Bob a Person?     True
```

---

**Q9. Create a `Counter` class that tracks how many objects have been created using a class attribute.**

✅ **Solution:**
```python
class Counter:
    count = 0    # Class attribute — shared by all objects

    def __init__(self, name):
        self.name  = name
        Counter.count += 1    # Increment on each new object
        self.id = Counter.count

    def display(self):
        print(f"  Object #{self.id}: {self.name}")

    @classmethod
    def get_count(cls):
        return f"Total objects created: {cls.count}"

    def __str__(self):
        return f"Counter(id={self.id}, name='{self.name}')"

# Test
print(Counter.get_count())

c1 = Counter("First")
c2 = Counter("Second")
c3 = Counter("Third")

c1.display()
c2.display()
c3.display()

print(Counter.get_count())
```

**Output:**
```
Total objects created: 0
  Object #1: First
  Object #2: Second
  Object #3: Third
Total objects created: 3
```

💡 **Key Tip:** `@classmethod` receives `cls` (the class itself) instead of `self` — useful for tracking class-level data.

---

**Q10. Create a `Temperature` class that stores temperature and converts between Celsius and Fahrenheit.**

✅ **Solution:**
```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    def to_fahrenheit(self):
        return round((self.celsius * 9/5) + 32, 2)

    def to_kelvin(self):
        return round(self.celsius + 273.15, 2)

    @staticmethod
    def from_fahrenheit(f):
        return Temperature(round((f - 32) * 5/9, 2))

    def __str__(self):
        return (f"{self.celsius}°C = "
                f"{self.to_fahrenheit()}°F = "
                f"{self.to_kelvin()}K")

# Test
temps = [0, 20, 37, 100, -40]

print(f"{'Celsius':>10} | {'Fahrenheit':>12} | {'Kelvin':>10}")
print("-" * 40)

for c in temps:
    t = Temperature(c)
    print(f"{c:>10}°C | {t.to_fahrenheit():>10}°F | {t.to_kelvin():>8}K")

# From Fahrenheit
print("\nConverting 98.6°F:")
t2 = Temperature.from_fahrenheit(98.6)
print(t2)
```

**Output:**
```
   Celsius |  Fahrenheit |     Kelvin
----------------------------------------
        0°C |       32.0°F |   273.15K
       20°C |       68.0°F |   293.15K
       37°C |       98.6°F |   310.15K
      100°C |      212.0°F |   373.15K
      -40°C |      -40.0°F |   233.15K

Converting 98.6°F:
37.0°C = 98.6°F = 310.15K
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Create a `Library` class that manages a collection of books — add, remove, search, and display.**

✅ **Solution:**
```python
class Book:
    def __init__(self, title, author, year):
        self.title  = title
        self.author = author
        self.year   = year

    def __str__(self):
        return f"'{self.title}' by {self.author} ({self.year})"


class Library:
    def __init__(self, name):
        self.name  = name
        self.books = []

    def add_book(self, book):
        self.books.append(book)
        print(f"  ✅ Added: {book}")

    def remove_book(self, title):
        for book in self.books:
            if book.title.lower() == title.lower():
                self.books.remove(book)
                print(f"  🗑️  Removed: {book}")
                return
        print(f"  ❌ Book '{title}' not found.")

    def search(self, keyword):
        results = [b for b in self.books
                   if keyword.lower() in b.title.lower()
                   or keyword.lower() in b.author.lower()]
        return results

    def display_all(self):
        print(f"\n📚 {self.name} — {len(self.books)} book(s):")
        if not self.books:
            print("  (empty)")
        else:
            for i, book in enumerate(self.books, 1):
                print(f"  {i}. {book}")


# Test
lib = Library("City Library")

lib.add_book(Book("Python Basics",    "John Smith",   2021))
lib.add_book(Book("Clean Code",       "Robert Martin",2008))
lib.add_book(Book("Data Structures",  "Alice Brown",  2019))
lib.add_book(Book("Python Advanced",  "John Smith",   2023))

lib.display_all()

print("\n🔍 Searching for 'Python':")
results = lib.search("Python")
for r in results:
    print(f"  → {r}")

print("\n🔍 Searching for 'John Smith':")
results = lib.search("John Smith")
for r in results:
    print(f"  → {r}")

lib.remove_book("Clean Code")
lib.remove_book("Unknown Book")

lib.display_all()
```

**Output:**
```
  ✅ Added: 'Python Basics' by John Smith (2021)
  ✅ Added: 'Clean Code' by Robert Martin (2008)
  ✅ Added: 'Data Structures' by Alice Brown (2019)
  ✅ Added: 'Python Advanced' by John Smith (2023)

📚 City Library — 4 book(s):
  1. 'Python Basics' by John Smith (2021)
  2. 'Clean Code' by Robert Martin (2008)
  3. 'Data Structures' by Alice Brown (2019)
  4. 'Python Advanced' by John Smith (2023)

🔍 Searching for 'Python':
  → 'Python Basics' by John Smith (2021)
  → 'Python Advanced' by John Smith (2023)

🔍 Searching for 'John Smith':
  → 'Python Basics' by John Smith (2021)
  → 'Python Advanced' by John Smith (2023)

  🗑️  Removed: 'Clean Code' by Robert Martin (2008)
  ❌ Book 'Unknown Book' not found.

📚 City Library — 3 book(s):
  1. 'Python Basics' by John Smith (2021)
  2. 'Data Structures' by Alice Brown (2019)
  3. 'Python Advanced' by John Smith (2023)
```

---

**Q12. Create a `Shape` base class with `area()` and `perimeter()` — inherit into `Rectangle`, `Circle`, and `Triangle`.**

✅ **Solution:**
```python
import math

class Shape:
    """Base class for all shapes."""
    def area(self):
        raise NotImplementedError("Subclass must implement area()")

    def perimeter(self):
        raise NotImplementedError("Subclass must implement perimeter()")

    def describe(self):
        print(f"  {self.__class__.__name__:<12} → "
              f"Area: {self.area():>8.2f} | "
              f"Perimeter: {self.perimeter():>8.2f}")


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return round(math.pi * self.radius ** 2, 2)

    def perimeter(self):
        return round(2 * math.pi * self.radius, 2)


class Triangle(Shape):
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c

    def area(self):
        # Heron's formula
        s = (self.a + self.b + self.c) / 2
        return round(math.sqrt(s * (s-self.a) * (s-self.b) * (s-self.c)), 2)

    def perimeter(self):
        return self.a + self.b + self.c


# Test — polymorphism in action
shapes = [
    Rectangle(5, 10),
    Circle(7),
    Triangle(3, 4, 5),
    Rectangle(8, 8),
    Circle(3),
]

print(f"  {'Shape':<12}   {'Area':>8}   {'Perimeter':>10}")
print("  " + "-" * 42)

for shape in shapes:
    shape.describe()
```

**Output:**
```
  Shape            Area    Perimeter
  ------------------------------------------
  Rectangle    →  Area:    50.00 | Perimeter:    30.00
  Circle       →  Area:   153.94 | Perimeter:    43.98
  Triangle     →  Area:     6.00 | Perimeter:    12.00
  Rectangle    →  Area:    64.00 | Perimeter:    32.00
  Circle       →  Area:    28.27 | Perimeter:    18.85
```

---

**Q13. Implement encapsulation — create an `Employee` class with private attributes and getter/setter methods.**

✅ **Solution:**
```python
class Employee:
    def __init__(self, name, employee_id, salary):
        self.name          = name
        self.__employee_id = employee_id   # Private
        self.__salary      = salary        # Private

    # Getter for salary
    def get_salary(self):
        return self.__salary

    # Setter for salary with validation
    def set_salary(self, new_salary):
        if new_salary < 0:
            print("  ❌ Salary cannot be negative.")
        elif new_salary < self.__salary:
            print(f"  ⚠️  Warning: Salary reduced from "
                  f"₹{self.__salary} to ₹{new_salary}")
            self.__salary = new_salary
        else:
            increase = new_salary - self.__salary
            self.__salary = new_salary
            print(f"  ✅ Salary updated. Increase: ₹{increase}")

    # Getter for employee_id (read-only — no setter)
    def get_employee_id(self):
        return self.__employee_id

    def display(self):
        print(f"  Name: {self.name:<12} | "
              f"ID: {self.__employee_id} | "
              f"Salary: ₹{self.__salary:,}")

    def __str__(self):
        return f"Employee({self.name}, ID={self.__employee_id})"


# Test
emp = Employee("Alice", "E001", 50000)
emp.display()

print()

# Use setter
emp.set_salary(60000)
emp.set_salary(45000)
emp.set_salary(-1000)

print()
emp.display()

# Try to access private attribute directly
try:
    print(emp.__salary)
except AttributeError as e:
    print(f"\n  ❌ Direct access blocked: {e}")

# Correct way — via getter
print(f"\n  Salary via getter: ₹{emp.get_salary():,}")
print(f"  ID via getter:     {emp.get_employee_id()}")
```

**Output:**
```
  Name: Alice        | ID: E001 | Salary: ₹50,000

  ✅ Salary updated. Increase: ₹10000
  ⚠️  Warning: Salary reduced from ₹60000 to ₹45000
  ❌ Salary cannot be negative.

  Name: Alice        | ID: E001 | Salary: ₹45,000

  ❌ Direct access blocked: 'Employee' object has no attribute '__salary'

  Salary via getter: ₹45,000
  ID via getter:     E001
```

💡 **Key Tip:** `__name` (double underscore) triggers **name mangling** — it becomes `_ClassName__name`, making it effectively private.

---

**Q14. Implement multilevel inheritance — `Animal` → `Mammal` → `Dog`.**

✅ **Solution:**
```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age  = age

    def breathe(self):
        return f"{self.name} is breathing."

    def eat(self):
        return f"{self.name} is eating."

    def __str__(self):
        return f"{self.__class__.__name__}(name={self.name}, age={self.age})"


class Mammal(Animal):
    def __init__(self, name, age, fur_color):
        super().__init__(name, age)
        self.fur_color = fur_color

    def feed_young(self):
        return f"{self.name} is feeding its young with milk."

    def describe(self):
        return (f"{self.name} is a mammal with "
                f"{self.fur_color} fur.")


class Dog(Mammal):
    def __init__(self, name, age, fur_color, breed):
        super().__init__(name, age, fur_color)
        self.breed = breed

    def speak(self):
        return f"{self.name} says: Woof! 🐕"

    def fetch(self, item):
        return f"{self.name} fetched the {item}!"

    def full_profile(self):
        print(f"  ── Dog Profile ──────────────────")
        print(f"  Name     : {self.name}")
        print(f"  Age      : {self.age} years")
        print(f"  Breed    : {self.breed}")
        print(f"  Fur Color: {self.fur_color}")
        print(f"  {self.breathe()}")
        print(f"  {self.feed_young()}")
        print(f"  {self.speak()}")
        print(f"  {self.fetch('ball')}")


# Test
dog = Dog("Rex", 3, "Golden", "Labrador")
dog.full_profile()

print()
print(f"  Is Dog a Mammal? {issubclass(Dog, Mammal)}")
print(f"  Is Dog an Animal?{issubclass(Dog, Animal)}")
print(f"  MRO: {[cls.__name__ for cls in Dog.__mro__]}")
```

**Output:**
```
  ── Dog Profile ──────────────────
  Name     : Rex
  Age      : 3 years
  Breed    : Labrador
  Fur Color: Golden
  Rex is breathing.
  Rex is feeding its young with milk.
  Rex says: Woof! 🐕
  Rex fetched the ball!

  Is Dog a Mammal?  True
  Is Dog an Animal? True
  MRO: ['Dog', 'Mammal', 'Animal', 'object']
```

💡 **Key Tip:** **MRO (Method Resolution Order)** defines the order Python looks for methods — `Dog → Mammal → Animal → object`.

---

**Q15. Create a `StudentGradeManager` class that uses OOP to manage students and calculate grades.**

✅ **Solution:**
```python
class Student:
    def __init__(self, name, student_id):
        self.name       = name
        self.student_id = student_id
        self.marks      = {}

    def add_marks(self, subject, score):
        self.marks[subject] = score

    def average(self):
        if not self.marks:
            return 0
        return round(sum(self.marks.values()) / len(self.marks), 2)

    def grade(self):
        avg = self.average()
        if   avg >= 90: return 'A+'
        elif avg >= 80: return 'A'
        elif avg >= 70: return 'B'
        elif avg >= 60: return 'C'
        elif avg >= 40: return 'D'
        else:           return 'F'

    def result(self):
        return "PASS ✅" if self.grade() != 'F' else "FAIL ❌"

    def report_card(self):
        print(f"  ┌─────────────────────────────┐")
        print(f"  │ Name   : {self.name:<20}│")
        print(f"  │ ID     : {self.student_id:<20}│")
        print(f"  ├─────────────────────────────┤")
        for subject, score in self.marks.items():
            print(f"  │ {subject:<10}: {score:<3}                  │")
        print(f"  ├─────────────────────────────┤")
        print(f"  │ Average: {self.average():<5}                │")
        print(f"  │ Grade  : {self.grade():<5}                │")
        print(f"  │ Result : {self.result():<20}│")
        print(f"  └─────────────────────────────┘")


class GradeManager:
    def __init__(self):
        self.students = []

    def add_student(self, student):
        self.students.append(student)

    def topper(self):
        return max(self.students, key=lambda s: s.average())

    def class_average(self):
        if not self.students:
            return 0
        return round(sum(s.average() for s in self.students)
                     / len(self.students), 2)

    def summary(self):
        print("\n  📊 CLASS SUMMARY")
        print(f"  {'Name':<12} | {'Avg':>5} | {'Grade':>5} | {'Result'}")
        print("  " + "-" * 45)
        for s in sorted(self.students,
                        key=lambda x: x.average(), reverse=True):
            print(f"  {s.name:<12} | {s.average():>5} | "
                  f"{s.grade():>5} | {s.result()}")
        print("  " + "-" * 45)
        print(f"  Class Average : {self.class_average()}")
        print(f"  Topper        : {self.topper().name} "
              f"({self.topper().average()})")


# Test
subjects = ['Python', 'Linux', 'Networks', 'Security']
data = [
    ("Alice",   "S001", [92, 88, 85, 90]),
    ("Bob",     "S002", [55, 60, 58, 62]),
    ("Charlie", "S003", [78, 72, 80, 75]),
    ("Diana",   "S004", [35, 40, 30, 38]),
    ("Eve",     "S005", [95, 92, 98, 96]),
]

manager = GradeManager()

for name, sid, scores in data:
    student = Student(name, sid)
    for subject, score in zip(subjects, scores):
        student.add_marks(subject, score)
    manager.add_student(student)

# Print one detailed report card
manager.students[4].report_card()

# Print class summary
manager.summary()
```

**Output:**
```
  ┌─────────────────────────────┐
  │ Name   : Eve                │
  │ ID     : S005               │
  ├─────────────────────────────┤
  │ Python   : 95               │
  │ Linux    : 92               │
  │ Networks : 98               │
  │ Security : 96               │
  ├─────────────────────────────┤
  │ Average: 95.25              │
  │ Grade  : A+                 │
  │ Result : PASS ✅            │
  └─────────────────────────────┘

  📊 CLASS SUMMARY
  Name         |   Avg | Grade | Result
  ---------------------------------------------
  Eve          | 95.25 |   A+  | PASS ✅
  Alice        | 88.75 |    A  | PASS ✅
  Charlie      | 76.25 |    B  | PASS ✅
  Bob          | 58.75 |    C  | PASS ✅
  Diana        | 35.75 |    F  | FAIL ❌
  ---------------------------------------------
  Class Average : 70.95
  Topper        : Eve (95.25)
```

---

---

## 🌐 Topic 10: Sockets

### 📋 Quick Reference

#### 🖥️ Server Side
| Step | Code | Description |
|---|---|---|
| 1 | `import socket` | Import module |
| 2 | `s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)` | Create TCP socket |
| 3 | `s.bind((host, port))` | Bind to address & port |
| 4 | `s.listen(n)` | Listen for connections (n = backlog) |
| 5 | `conn, addr = s.accept()` | Accept incoming connection |
| 6 | `data = conn.recv(1024)` | Receive data (buffer size) |
| 7 | `conn.send(data)` | Send data |
| 8 | `conn.close()` | Close connection |

#### 💻 Client Side
| Step | Code | Description |
|---|---|---|
| 1 | `import socket` | Import module |
| 2 | `s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)` | Create TCP socket |
| 3 | `s.connect((host, port))` | Connect to server |
| 4 | `s.send(b"Hello")` | Send bytes |
| 5 | `data = s.recv(1024)` | Receive response |
| 6 | `s.close()` | Close socket |

#### 🔑 Key Constants
| Constant | Meaning |
|---|---|
| `socket.AF_INET` | IPv4 Address Family |
| `socket.AF_INET6` | IPv6 Address Family |
| `socket.SOCK_STREAM` | TCP (reliable, connection-based) |
| `socket.SOCK_DGRAM` | UDP (fast, connectionless) |

---

### 🟢 Q1–Q5: Understanding

---

**Q1. What is a Socket? Explain the Client-Server model.**

✅ **Answer:**
- A **socket** is a communication endpoint — it allows two programs to **send and receive data** over a network.
- Python's `socket` module provides low-level networking.

```
CLIENT ──────────────────── SERVER
  │                             │
  │  1. Server creates socket   │
  │  2. Server binds to port    │
  │  3. Server listens          │
  │  4. Client creates socket   │
  │  5. Client connects ───────►│
  │  6. Server accepts ◄────────│
  │  7. Client sends ──────────►│
  │  8. Server receives         │
  │  9. Server sends ◄──────────│
  │  10. Client receives        │
  │  11. Both close connection  │
```

💡 **Key Tip:** `AF_INET` + `SOCK_STREAM` = **TCP socket** — the most common type, reliable and ordered.

---

**Q2. What is the output / what does each line do?**

```python
import socket

# Explain each line:
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(('localhost', 9999))
s.listen(5)
print("Server is listening on port 9999...")

conn, addr = s.accept()     # Line A
print(f"Connected to: {addr}")

data = conn.recv(1024)      # Line B
print(f"Received: {data.decode()}")

conn.send(b"Hello Client!") # Line C
conn.close()                # Line D
```

✅ **Answer:**

| Line | What it does |
|---|---|
| `socket.socket(...)` | Creates a **TCP IPv4** socket object |
| `s.bind(...)` | Binds the socket to `localhost` on port `9999` |
| `s.listen(5)` | Starts listening — allows up to **5 queued connections** |
| `s.accept()` — Line A | **Blocks and waits** until a client connects — returns `(conn, addr)` |
| `conn.recv(1024)` — Line B | Receives up to **1024 bytes** of data from client |
| `conn.send(b"...")` — Line C | Sends **bytes** back to the client |
| `conn.close()` — Line D | Closes the **client connection** |

💡 **Key Tip:** `recv()` and `send()` work with **bytes** (`b"..."`) — always encode/decode strings.

---

**Q3. True or False — with reason.**

```
a) socket.AF_INET is used for IPv6 connections.
b) s.bind() is used on the SERVER side.
c) s.connect() is used on the CLIENT side.
d) Data sent via sockets must be in bytes format.
```

✅ **Answer:**

| Statement | Answer | Reason |
|---|---|---|
| a) `AF_INET` for IPv6 | ❌ False | `AF_INET` = **IPv4**; use `AF_INET6` for IPv6 |
| b) `bind()` on server | ✅ True | Server **binds** to a host/port to listen on |
| c) `connect()` on client | ✅ True | Client **connects** to the server's address/port |
| d) Data must be bytes | ✅ True | Use `.encode()` / `.decode()` to convert strings |

---

**Q4. Fill in the blank — Complete the server and client code.**

```python
# ── SERVER ──────────────────────────────
import socket

server = socket.socket(socket.______, socket.______)
server.bind(('______', ______))
server.______(1)

print("Waiting for connection...")
conn, addr = server.______()
print(f"Connected: {addr}")

data = conn.______(1024)
print(f"Client says: {data.______()}")

conn.______(b"Message received!")
conn.______()
server.______()

# ── CLIENT ──────────────────────────────
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.______('localhost', 5000)

client.______(b"Hello Server!")

response = client.______(1024)
print(f"Server says: {response.decode()}")

client.______()
```

✅ **Answer:**

```python
# ── SERVER ──────────────────────────────
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('localhost', 5000))
server.listen(1)

print("Waiting for connection...")
conn, addr = server.accept()
print(f"Connected: {addr}")

data = conn.recv(1024)
print(f"Client says: {data.decode()}")

conn.send(b"Message received!")
conn.close()
server.close()

# ── CLIENT ──────────────────────────────
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(('localhost', 5000))

client.send(b"Hello Server!")

response = client.recv(1024)
print(f"Server says: {response.decode()}")

client.close()
```

---

**Q5. What is the difference between TCP and UDP sockets?**

✅ **Answer:**

| Feature | TCP (`SOCK_STREAM`) | UDP (`SOCK_DGRAM`) |
|---|---|---|
| Connection | Connection-based | Connectionless |
| Reliability | ✅ Guaranteed delivery | ❌ Not guaranteed |
| Order | ✅ Data arrives in order | ❌ No guaranteed order |
| Speed | Slower (overhead) | Faster (no handshake) |
| Use Case | Web, File Transfer, Chat | Video streaming, DNS, Games |
| Python constant | `socket.SOCK_STREAM` | `socket.SOCK_DGRAM` |

```python
import socket

# TCP Socket
tcp = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# UDP Socket
udp = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
```

💡 **Key Tip:** For exam/lab purposes, almost all programs use **TCP** (`SOCK_STREAM`) — it's the default for most network applications.

---

### 🔵 Q6–Q10: Basic Programs

> ⚠️ **Note:** For all socket programs below, run the **Server first** in one terminal, then run the **Client** in a second terminal.

---

**Q6. Write a basic TCP Server and Client that exchange a single message.**

✅ **Solution:**

```python
# ══ FILE: server.py ══════════════════════════════
import socket

HOST = 'localhost'
PORT = 5000

# Step 1: Create socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Step 2: Bind
server.bind((HOST, PORT))

# Step 3: Listen
server.listen(1)
print(f"[SERVER] Listening on {HOST}:{PORT}...")

# Step 4: Accept
conn, addr = server.accept()
print(f"[SERVER] Connected by {addr}")

# Step 5: Receive
data = conn.recv(1024)
print(f"[SERVER] Received: {data.decode()}")

# Step 6: Send reply
conn.send(b"Hello from Server!")

# Step 7: Close
conn.close()
server.close()
print("[SERVER] Connection closed.")
```

```python
# ══ FILE: client.py ══════════════════════════════
import socket

HOST = 'localhost'
PORT = 5000

# Step 1: Create socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Step 2: Connect
client.connect((HOST, PORT))
print(f"[CLIENT] Connected to {HOST}:{PORT}")

# Step 3: Send
client.send(b"Hello from Client!")
print("[CLIENT] Message sent.")

# Step 4: Receive reply
response = client.recv(1024)
print(f"[CLIENT] Server replied: {response.decode()}")

# Step 5: Close
client.close()
print("[CLIENT] Connection closed.")
```

**Server Terminal Output:**
```
[SERVER] Listening on localhost:5000...
[SERVER] Connected by ('127.0.0.1', 54321)
[SERVER] Received: Hello from Client!
[SERVER] Connection closed.
```

**Client Terminal Output:**
```
[CLIENT] Connected to localhost:5000
[CLIENT] Message sent.
[CLIENT] Server replied: Hello from Server!
[CLIENT] Connection closed.
```

---

**Q7. Write a server that sends the current date and time to a client.**

✅ **Solution:**

```python
# ══ FILE: time_server.py ═════════════════════════
import socket
from datetime import datetime

HOST = 'localhost'
PORT = 5001

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen(1)
print(f"[TIME SERVER] Listening on port {PORT}...")

conn, addr = server.accept()
print(f"[TIME SERVER] Client connected: {addr}")

# Get current datetime
now = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
message = f"Server Time: {now}"

conn.send(message.encode())
print(f"[TIME SERVER] Sent: {message}")

conn.close()
server.close()
```

```python
# ══ FILE: time_client.py ═════════════════════════
import socket

HOST = 'localhost'
PORT = 5001

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print(f"[CLIENT] Connected to Time Server.")

data = client.recv(1024)
print(f"[CLIENT] Received: {data.decode()}")

client.close()
```

**Output:**
```
[TIME SERVER] Listening on port 5001...
[TIME SERVER] Client connected: ('127.0.0.1', 54322)
[TIME SERVER] Sent: Server Time: 2026-06-04 10:30:45

[CLIENT] Connected to Time Server.
[CLIENT] Received: Server Time: 2026-06-04 10:30:45
```

---

**Q8. Write a server that receives a number from the client and sends back its square.**

✅ **Solution:**

```python
# ══ FILE: square_server.py ═══════════════════════
import socket

HOST = 'localhost'
PORT = 5002

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen(1)
print(f"[SQUARE SERVER] Ready on port {PORT}...")

conn, addr = server.accept()
print(f"[SQUARE SERVER] Client: {addr}")

# Receive number
data = conn.recv(1024).decode()
print(f"[SQUARE SERVER] Received number: {data}")

# Calculate square
try:
    number = float(data)
    result = number ** 2
    response = f"Square of {number} = {result}"
except ValueError:
    response = "ERROR: Not a valid number"

conn.send(response.encode())
print(f"[SQUARE SERVER] Sent: {response}")

conn.close()
server.close()
```

```python
# ══ FILE: square_client.py ═══════════════════════
import socket

HOST = 'localhost'
PORT = 5002

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

number = input("[CLIENT] Enter a number: ")
client.send(number.encode())

response = client.recv(1024).decode()
print(f"[CLIENT] Server says: {response}")

client.close()
```

**Output:**
```
[CLIENT] Enter a number: 12
[CLIENT] Server says: Square of 12.0 = 144.0
```

---

**Q9. Write a server that receives a string and sends it back in UPPERCASE.**

✅ **Solution:**

```python
# ══ FILE: upper_server.py ════════════════════════
import socket

HOST = 'localhost'
PORT = 5003

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)
print(f"[UPPER SERVER] Listening on port {PORT}...")

conn, addr = server.accept()
print(f"[UPPER SERVER] Connected: {addr}")

# Receive string
message = conn.recv(1024).decode()
print(f"[UPPER SERVER] Received: '{message}'")

# Convert to uppercase and send back
upper = message.upper()
conn.send(upper.encode())
print(f"[UPPER SERVER] Sent back: '{upper}'")

conn.close()
server.close()
```

```python
# ══ FILE: upper_client.py ════════════════════════
import socket

HOST = 'localhost'
PORT = 5003

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

text = input("[CLIENT] Enter a message: ")
client.send(text.encode())

response = client.recv(1024).decode()
print(f"[CLIENT] Server returned: '{response}'")

client.close()
```

**Output:**
```
[CLIENT] Enter a message: hello world python
[CLIENT] Server returned: 'HELLO WORLD PYTHON'
```

💡 **Key Tip:** `server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)` allows the server to **reuse the port immediately** after closing — useful during development.

---

**Q10. Write a client that gets the hostname and IP address of a given domain.**

✅ **Solution:**

```python
# ══ FILE: dns_lookup.py ══════════════════════════
import socket

def dns_lookup(domain):
    print(f"\n🔍 DNS Lookup: {domain}")
    print("-" * 40)

    try:
        # Get IP address
        ip = socket.gethostbyname(domain)
        print(f"  IP Address   : {ip}")

        # Get full host info
        host_info = socket.gethostbyname_ex(domain)
        print(f"  Hostname     : {host_info[0]}")
        print(f"  Aliases      : {host_info[1] if host_info[1] else 'None'}")
        print(f"  All IPs      : {host_info[2]}")

    except socket.gaierror as e:
        print(f"  ❌ Error: {e}")

def get_local_info():
    print("\n💻 Local Machine Info")
    print("-" * 40)
    hostname = socket.gethostname()
    local_ip = socket.gethostbyname(hostname)
    print(f"  Hostname : {hostname}")
    print(f"  Local IP : {local_ip}")

# Test
get_local_info()

domains = ["google.com", "github.com", "invalid.xyz.abc"]
for domain in domains:
    dns_lookup(domain)
```

**Output:**
```
💻 Local Machine Info
----------------------------------------
  Hostname : MyComputer
  Local IP : 192.168.1.10

🔍 DNS Lookup: google.com
----------------------------------------
  IP Address   : 142.250.182.46
  Hostname     : google.com
  Aliases      : None
  All IPs      : ['142.250.182.46']

🔍 DNS Lookup: github.com
----------------------------------------
  IP Address   : 140.82.112.4
  Hostname     : github.com
  Aliases      : None
  All IPs      : ['140.82.112.4']

🔍 DNS Lookup: invalid.xyz.abc
----------------------------------------
  ❌ Error: [Errno 11001] getaddrinfo failed
```

---

### 🟡 Q11–Q15: Medium Programs

---

**Q11. Write a multi-message chat between a server and client — they take turns sending messages until "exit" is typed.**

✅ **Solution:**

```python
# ══ FILE: chat_server.py ═════════════════════════
import socket

HOST = 'localhost'
PORT = 5004

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)
print(f"[SERVER] Chat server ready on port {PORT}...")
print("[SERVER] Waiting for client...\n")

conn, addr = server.accept()
print(f"[SERVER] Client connected: {addr}")
print("[SERVER] Type 'exit' to end the chat.\n")

while True:
    # Receive from client
    data = conn.recv(1024).decode()
    if not data or data.lower() == 'exit':
        print("[SERVER] Client disconnected.")
        break
    print(f"[CLIENT]: {data}")

    # Send to client
    reply = input("[SERVER]: ")
    conn.send(reply.encode())
    if reply.lower() == 'exit':
        print("[SERVER] Ending chat.")
        break

conn.close()
server.close()
```

```python
# ══ FILE: chat_client.py ═════════════════════════
import socket

HOST = 'localhost'
PORT = 5004

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print(f"[CLIENT] Connected to chat server!")
print("[CLIENT] Type 'exit' to end the chat.\n")

while True:
    # Send to server
    message = input("[CLIENT]: ")
    client.send(message.encode())
    if message.lower() == 'exit':
        print("[CLIENT] Ending chat.")
        break

    # Receive from server
    response = client.recv(1024).decode()
    if not response or response.lower() == 'exit':
        print("[SERVER] Server disconnected.")
        break
    print(f"[SERVER]: {response}")

client.close()
```

**Sample Terminal Output:**
```
── Client Terminal ──         ── Server Terminal ──
[CLIENT]: Hello Server!       [CLIENT]: Hello Server!
[SERVER]: Hi! How are you?    [SERVER]: Hi! How are you?
[CLIENT]: I'm good thanks!    [CLIENT]: I'm good thanks!
[SERVER]: Great to hear!      [SERVER]: Great to hear!
[CLIENT]: exit                [SERVER] Client disconnected.
[CLIENT] Ending chat.
```

---

**Q12. Write a server that handles a client sending a string, then responds with word count, character count, and reversed string.**

✅ **Solution:**

```python
# ══ FILE: text_analyze_server.py ═════════════════
import socket

HOST = 'localhost'
PORT = 5005

def analyze_text(text):
    word_count = len(text.split())
    char_count = len(text)
    char_no_space = len(text.replace(" ", ""))
    reversed_text = text[::-1]

    result = (
        f"\n📊 Text Analysis Results:\n"
        f"  Original      : {text}\n"
        f"  Word Count    : {word_count}\n"
        f"  Char Count    : {char_count}\n"
        f"  Chars(no space): {char_no_space}\n"
        f"  Reversed      : {reversed_text}"
    )
    return result

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)
print(f"[TEXT SERVER] Listening on port {PORT}...")

conn, addr = server.accept()
print(f"[TEXT SERVER] Client connected: {addr}")

text = conn.recv(4096).decode()
print(f"[TEXT SERVER] Received: '{text}'")

result = analyze_text(text)
conn.send(result.encode())
print("[TEXT SERVER] Analysis sent.")

conn.close()
server.close()
```

```python
# ══ FILE: text_analyze_client.py ═════════════════
import socket

HOST = 'localhost'
PORT = 5005

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print("[CLIENT] Connected to Text Analysis Server.")

text = input("[CLIENT] Enter text to analyze: ")
client.send(text.encode())

result = client.recv(4096).decode()
print(f"[CLIENT] Server Response:{result}")

client.close()
```

**Output:**
```
[CLIENT] Enter text to analyze: Hello World from Python

[CLIENT] Server Response:
📊 Text Analysis Results:
  Original       : Hello World from Python
  Word Count     : 4
  Char Count     : 22
  Chars(no space): 19
  Reversed       : nohtyP morf dlroW olleH
```

---

**Q13. Write a file transfer program — client sends a text file to the server, server saves it.**

✅ **Solution:**

```python
# ══ FILE: file_server.py ═════════════════════════
import socket
import os

HOST = 'localhost'
PORT = 5006
SAVE_DIR = "received_files"

# Create directory if not exists
os.makedirs(SAVE_DIR, exist_ok=True)

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(1)
print(f"[FILE SERVER] Listening on port {PORT}...")

conn, addr = server.accept()
print(f"[FILE SERVER] Client connected: {addr}")

# Step 1: Receive filename
filename = conn.recv(1024).decode()
print(f"[FILE SERVER] Receiving file: '{filename}'")
conn.send(b"READY")  # Acknowledge

# Step 2: Receive file content
content = b""
while True:
    chunk = conn.recv(4096)
    if chunk == b"EOF":  # End of file signal
        break
    content += chunk

# Step 3: Save the file
save_path = os.path.join(SAVE_DIR, filename)
with open(save_path, 'wb') as f:
    f.write(content)

print(f"[FILE SERVER] File saved to '{save_path}'")
print(f"[FILE SERVER] Size: {len(content)} bytes")

conn.send(b"FILE RECEIVED")
conn.close()
server.close()
```

```python
# ══ FILE: file_client.py ═════════════════════════
import socket
import os

HOST = 'localhost'
PORT = 5006

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))
print("[CLIENT] Connected to File Server.")

# File to send
filename = input("[CLIENT] Enter filename to send: ")

if not os.path.exists(filename):
    print(f"[CLIENT] ❌ File '{filename}' not found!")
    client.close()
    exit()

# Step 1: Send filename
client.send(os.path.basename(filename).encode())
ack = client.recv(1024)
print(f"[CLIENT] Server response: {ack.decode()}")

# Step 2: Send file content
with open(filename, 'rb') as f:
    while True:
        chunk = f.read(4096)
        if not chunk:
            break
        client.send(chunk)

# Step 3: Send EOF signal
client.send(b"EOF")

# Wait for confirmation
confirm = client.recv(1024).decode()
print(f"[CLIENT] {confirm}")
print(f"[CLIENT] File '{filename}' sent successfully!")

client.close()
```

**Output:**
```
── Client Terminal ──
[CLIENT] Connected to File Server.
[CLIENT] Enter filename to send: notes.txt
[CLIENT] Server response: READY
[CLIENT] FILE RECEIVED
[CLIENT] File 'notes.txt' sent successfully!

── Server Terminal ──
[FILE SERVER] Listening on port 5006...
[FILE SERVER] Client connected: ('127.0.0.1', 54325)
[FILE SERVER] Receiving file: 'notes.txt'
[FILE SERVER] File saved to 'received_files/notes.txt'
[FILE SERVER] Size: 1024 bytes
```

---

**Q14. Write a server that accepts a client's request and serves back the content of a webpage (simple HTTP-like server).**

✅ **Solution:**

```python
# ══ FILE: webpage_server.py ══════════════════════
import socket

HOST = 'localhost'
PORT = 5007

# Simple HTML page to serve
HTML_CONTENT = """<!DOCTYPE html>
<html>
  <head><title>Python Socket Server</title></head>
  <body>
    <h1>Hello from Python Socket Server!</h1>
    <p>This page was served by a raw Python socket.</p>
    <p>Server: localhost:{}</p>
  </body>
</html>""".format(PORT)

# Build HTTP response
HTTP_RESPONSE = (
    "HTTP/1.1 200 OK\r\n"
    "Content-Type: text/html\r\n"
    f"Content-Length: {len(HTML_CONTENT)}\r\n"
    "Connection: close\r\n"
    "\r\n"
    + HTML_CONTENT
)

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
server.bind((HOST, PORT))
server.listen(5)
print(f"[WEB SERVER] Running at http://{HOST}:{PORT}/")
print("[WEB SERVER] Open your browser or run client.py\n")

while True:
    conn, addr = server.accept()
    print(f"[WEB SERVER] Request from: {addr}")

    request = conn.recv(4096).decode()
    request_line = request.split('\n')[0]
    print(f"[WEB SERVER] Request: {request_line}")

    conn.send(HTTP_RESPONSE.encode())
    conn.close()
    print(f"[WEB SERVER] Response sent.\n")
```

```python
# ══ FILE: webpage_client.py ══════════════════════
import socket

HOST = 'localhost'
PORT = 5007

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

# Send HTTP GET request
http_request = (
    f"GET / HTTP/1.1\r\n"
    f"Host: {HOST}:{PORT}\r\n"
    f"Connection: close\r\n"
    f"\r\n"
)

client.send(http_request.encode())
print("[CLIENT] HTTP GET request sent.\n")

# Receive response
response = b""
while True:
    chunk = client.recv(4096)
    if not chunk:
        break
    response += chunk

response_text = response.decode()

# Split headers and body
if "\r\n\r\n" in response_text:
    headers, body = response_text.split("\r\n\r\n", 1)
    print("[CLIENT] Response Headers:")
    for line in headers.split("\r\n"):
        print(f"  {line}")
    print("\n[CLIENT] Response Body:")
    print(body)

client.close()
```

**Output:**
```
[CLIENT] HTTP GET request sent.

[CLIENT] Response Headers:
  HTTP/1.1 200 OK
  Content-Type: text/html
  Content-Length: 198
  Connection: close

[CLIENT] Response Body:
<!DOCTYPE html>
<html>
  <head><title>Python Socket Server</title></head>
  <body>
    <h1>Hello from Python Socket Server!</h1>
    <p>This page was served by a raw Python socket.</p>
    <p>Server: localhost:5007</p>
  </body>
</html>
```

---

**Q15. Write a multi-client server using threading — handles multiple clients simultaneously.**

✅ **Solution:**

```python
# ══ FILE: threaded_server.py ═════════════════════
import socket
import threading

HOST = 'localhost'
PORT = 5008

# Track connected clients
clients      = []
clients_lock = threading.Lock()

def handle_client(conn, addr, client_id):
    """Handle one client in its own thread."""
    print(f"[SERVER] Client #{client_id} connected: {addr}")

    # Send welcome message
    conn.send(f"Welcome Client #{client_id}! "
              f"Send messages or 'exit' to quit.".encode())

    while True:
        try:
            data = conn.recv(1024)
            if not data:
                break

            message = data.decode()
            print(f"[CLIENT #{client_id}]: {message}")

            if message.lower() == 'exit':
                conn.send(b"Goodbye!")
                break

            # Echo back with uppercase transformation
            response = f"[Echo #{client_id}]: {message.upper()}"
            conn.send(response.encode())

        except ConnectionResetError:
            break

    # Clean up
    with clients_lock:
        if conn in clients:
            clients.remove(conn)

    conn.close()
    print(f"[SERVER] Client #{client_id} disconnected. "
          f"Active: {len(clients)}")


def start_server():
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind((HOST, PORT))
    server.listen(5)

    print(f"[SERVER] Threaded server on {HOST}:{PORT}")
    print("[SERVER] Waiting for clients...\n")

    client_id = 0

    while True:
        conn, addr = server.accept()
        client_id += 1

        with clients_lock:
            clients.append(conn)

        print(f"[SERVER] Active connections: {len(clients)}")

        # Each client gets its own thread
        thread = threading.Thread(
            target=handle_client,
            args=(conn, addr, client_id),
            daemon=True
        )
        thread.start()


start_server()
```

```python
# ══ FILE: threaded_client.py ═════════════════════
import socket

HOST = 'localhost'
PORT = 5008

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

# Receive welcome message
welcome = client.recv(1024).decode()
print(f"[SERVER]: {welcome}\n")

while True:
    message = input("[YOU]: ")
    client.send(message.encode())

    response = client.recv(1024).decode()
    print(f"[SERVER]: {response}")

    if message.lower() == 'exit':
        print("[CLIENT] Disconnected.")
        break

client.close()
```

**Output (3 clients running simultaneously):**
```
── Server Terminal ──────────────────────────────────
[SERVER] Threaded server on localhost:5008
[SERVER] Waiting for clients...

[SERVER] Active connections: 1
[SERVER] Client #1 connected: ('127.0.0.1', 54401)
[SERVER] Active connections: 2
[SERVER] Client #2 connected: ('127.0.0.1', 54402)
[CLIENT #1]: hello
[CLIENT #2]: testing
[CLIENT #1]: exit
[SERVER] Client #1 disconnected. Active: 1

── Client #1 Terminal ───────────────────────────────
[SERVER]: Welcome Client #1! Send messages or 'exit' to quit.
[YOU]: hello
[SERVER]: [Echo #1]: HELLO
[YOU]: exit
[SERVER]: Goodbye!
[CLIENT] Disconnected.

── Client #2 Terminal ───────────────────────────────
[SERVER]: Welcome Client #2! Send messages or 'exit' to quit.
[YOU]: testing
[SERVER]: [Echo #2]: TESTING
```

💡 **Step-by-step (Threading):**
1. Server accepts a connection
2. Creates a **new thread** for that client → `threading.Thread(target=handle_client, ...)`
3. Main loop continues accepting **new clients** without blocking
4. Each thread independently handles its own client
5. This is how real servers handle **multiple simultaneous connections**

---

---

## 📊 Part 3 Summary

| Topic | Q1–Q5 | Q6–Q10 | Q11–Q15 | Total |
|---|---|---|---|---|
| 🏛️ Classes & Objects | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| 🌐 Sockets | ✅ 5 | ✅ 5 | ✅ 5 | **15** |
| | | | **TOTAL** | **30 Questions** |

---

> 💡 **Exam Tips:**
>
> **OOP — Remember These:**
> - `__init__` = constructor → auto-called on object creation
> - `self` = reference to current object instance
> - `super().__init__()` = call parent constructor in child class
> - `__str__` = controls what `print(obj)` displays
> - **Encapsulation** → `__private` | **Inheritance** → `class Child(Parent):`
> - **Polymorphism** → same method name, different behavior in each class
>
> **Sockets — Remember These:**
> - **Server flow** → `socket()` → `bind()` → `listen()` → `accept()` → `recv()`/`send()` → `close()`
> - **Client flow** → `socket()` → `connect()` → `send()`/`recv()` → `close()`
> - Always send/receive **bytes** → use `.encode()` and `.decode()`
> - `AF_INET` + `SOCK_STREAM` = **TCP** (exam default)
> - `setsockopt(SO_REUSEADDR, 1)` → prevents "Address already in use" error
> - Use `threading` for handling multiple clients simultaneously

---

## 🏁 Complete Series Summary

| Part | File | Topics | Questions |
|---|---|---|---|
| **Part 1** | `Part1_DataStructures.md` | Dict, List, Tuple, Set, String | **75** |
| **Part 2** | `Part2_Functions.md` | Functions, Lambda/Map/Filter, Regex | **45** |
| **Part 3** | `Part3_OOP_Sockets.md` | OOP, Sockets | **30** |
| | | **GRAND TOTAL** | **150 Questions** |

---

*📁 Part of: Python-Exam-Prep Series | PGCP-ITISS | February 2026*
*⬅️ Previous: [Part 2 — Functions, Lambda/Map/Filter, Regex](Part2_Functions.md)*
*🏠 Index: [README.md](README.md)*