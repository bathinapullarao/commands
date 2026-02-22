# Python Topics Roadmap 🐍

A structured list of Python topics from basics to advanced, useful for interviews, DevOps, cloud, and data engineering.

---

## 1. Basics (Fundamentals)

- Python installation & setup  
- Variables & data types  
- Type casting  
- Input / Output  
- Comments & indentation  
- Keywords  

### Data Types
- int, float  
- string  
- boolean  
- list  
- tuple  
- set  
- dictionary  

---

## 2. Operators

- Arithmetic  
- Comparison  
- Logical  
- Assignment  
- Bitwise  
- Membership (`in`)  
- Identity (`is`)  

---

## 3. Control Flow

- if / else / elif  
- Nested conditions  
- for loop  
- while loop  
- break / continue / pass  

---

## 4. Functions

- Function definition  
- Parameters & arguments  
- Default arguments  
- Keyword arguments  
- *args, **kwargs  
- Lambda functions  
- Recursion  

---

## 5. Data Structures

### Lists
- append, extend, insert  
- remove, pop  
- slicing  

### Tuples
- Immutable collections  

### Sets
- Unique values  
- union, intersection  

### Dictionaries
- key-value pairs  
- get(), keys(), values()  

---

## 6. Strings

- Indexing & slicing  
- String methods  
- split, join  
- replace  
- formatting (f-strings)  

---

## 7. File Handling

- Open / read / write files  
- Text vs binary  
- with statement  

Example:
```python
with open("file.txt", "r") as f:
    data = f.read()
```

---

## 8. Exception Handling

- try / except  
- finally  
- raise  
- Custom exceptions  

---

## 9. Modules & Packages

- import  
- from … import  
- Built-in modules (os, sys, math)  
- Creating custom modules  

---

## 10. OOP (Object-Oriented Programming)

- Classes & objects  
- __init__ constructor  
- Inheritance  
- Polymorphism  
- Encapsulation  
- Abstraction  

---

## 11. Advanced Python

- List comprehensions  
- Dictionary comprehensions  
- Generators & yield  
- Decorators  
- Iterators  
- Context managers  

---

## 12. Data Handling Libraries

- NumPy  
- Pandas  
- Matplotlib  
- Seaborn  

---

## 13. Automation & DevOps Python

- OS automation (os, subprocess)  
- File processing  
- Log parsing  
- API calls (requests)  
- YAML/JSON handling  
- SSH automation (paramiko)  

---

## 14. Cloud & Infrastructure Python

- GCP SDK (google-cloud)  
- AWS boto3  
- Azure SDK  
- Terraform automation scripts  

---

## 15. Web & API Development

- Flask  
- FastAPI  
- Django  
- REST APIs  
- Authentication  

---

## 16. Multithreading & Parallelism

- threading  
- multiprocessing  
- asyncio  

---

## 17. Testing

- unittest  
- pytest  
- mocking  

---

## 18. Packaging & Deployment

- pip  
- virtualenv  
- requirements.txt  
- Dockerizing Python apps  

---

## Interview Focus Areas

- Data structures  
- OOP concepts  
- File handling  
- Exception handling  
- Comprehensions  
- Generators  
- Modules  
- API calls  
- JSON/YAML parsing  

---

# Python Topics — 2 Example Programs + Sample Outputs (with comments)

> Notes  
> - Outputs shown are **sample outputs** (your exact output may vary slightly).  
> - All programs are small, executable, and include **comment lines explaining the logic**.

---

## 1) Basics (Fundamentals)

### Example 1: Variables, types, casting
```python
# Example: store values, print their types, and cast types
name = "Ravi"          # string
age = 40               # int
height = 5.9           # float
is_devops = True       # bool

print(type(name), type(age), type(height), type(is_devops))

# Casting: convert int to string (useful for concatenation)
age_str = str(age)
print("Age as string:", age_str)
```
**Sample output**
```text
<class 'str'> <class 'int'> <class 'float'> <class 'bool'>
Age as string: 40
```

### Example 2: Input and output
```python
# Example: take input from user and print a formatted message
user = input("Enter your name: ")  # reads input as string
print(f"Hello, {user}!")           # f-string formatting
```
**Sample output**
```text
Enter your name: Archita
Hello, Archita!
```

---

## 2) Operators

### Example 1: Arithmetic + comparison
```python
# Example: arithmetic and comparison operators
a = 10
b = 3

print("a+b =", a + b)     # addition
print("a//b =", a // b)   # floor division
print("a%b =", a % b)     # remainder

print("a > b ?", a > b)   # comparison
```
**Sample output**
```text
a+b = 13
a//b = 3
a%b = 1
a > b ? True
```

### Example 2: Logical, membership, identity
```python
# Example: logical operators, membership, and identity
x = 5
nums = [1, 5, 9]

print(x > 0 and x < 10)     # logical AND
print(x in nums)            # membership
print(nums is nums)         # identity (same object)
```
**Sample output**
```text
True
True
True
```

---

## 3) Control Flow

### Example 1: if/elif/else
```python
# Example: categorize a number
n = 7

if n < 0:
    print("negative")
elif n == 0:
    print("zero")
else:
    print("positive")
```
**Sample output**
```text
positive
```

### Example 2: loops + break/continue
```python
# Example: print odd numbers until 7
for i in range(1, 11):
    if i % 2 == 0:
        continue          # skip even numbers
    print(i)
    if i == 7:
        break             # stop loop when i is 7
```
**Sample output**
```text
1
3
5
7
```

---

## 4) Functions

### Example 1: function with parameters and return
```python
# Example: function to compute area of rectangle
def area_rect(length, width):
    # Multiply length and width to get area
    return length * width

print(area_rect(5, 4))
```
**Sample output**
```text
20
```

### Example 2: *args and **kwargs
```python
# Example: sum any number of values using *args
def add_all(*nums):
    # nums is a tuple of all positional arguments
    return sum(nums)

# Example: print settings using **kwargs
def show_settings(**kwargs):
    # kwargs is a dict of key=value pairs
    for k, v in kwargs.items():
        print(k, "=", v)

print(add_all(1, 2, 3, 4))
show_settings(env="prod", region="europe-west2")
```
**Sample output**
```text
10
env = prod
region = europe-west2
```

---

## 5) Data Structures

### Example 1: list operations
```python
# Example: basic list operations
items = ["a", "b"]
items.append("c")       # add at end
items.insert(1, "x")    # insert at index 1
print(items)
items.pop()             # remove last
print(items)
```
**Sample output**
```text
['a', 'x', 'b', 'c']
['a', 'x', 'b']
```

### Example 2: dict operations
```python
# Example: dictionary operations
user = {"name": "Ravi", "role": "DevOps"}
user["city"] = "Hyderabad"          # add new key
print(user.get("role"))             # safe get
print(list(user.keys()))            # all keys
```
**Sample output**
```text
DevOps
['name', 'role', 'city']
```

---

## 6) Strings

### Example 1: slicing + methods
```python
# Example: slicing and methods
s = "  hello spark  "
print(s.strip())           # remove spaces
print(s.upper())           # uppercase
print(s[2:7])              # slice
```
**Sample output**
```text
hello spark
  HELLO SPARK  
hello
```

### Example 2: split/join + f-strings
```python
# Example: split and join
text = "a,b,c"
parts = text.split(",")    # split by comma
print(parts)

joined = "-".join(parts)   # join using '-'
print(f"joined={joined}")  # f-string
```
**Sample output**
```text
['a', 'b', 'c']
joined=a-b-c
```

---

## 7) File Handling

### Example 1: write then read a file
```python
# Example: write to a file and read it back
path = "demo.txt"

# 'with' auto-closes the file (safe)
with open(path, "w", encoding="utf-8") as f:
    f.write("hello\nworld\n")

with open(path, "r", encoding="utf-8") as f:
    print(f.read())
```
**Sample output**
```text
hello
world
```

### Example 2: read line-by-line
```python
# Example: read file line-by-line and count lines
path = "demo.txt"
count = 0

with open(path, "r", encoding="utf-8") as f:
    for line in f:
        count += 1
        print(line.strip())  # strip newline

print("lines:", count)
```
**Sample output**
```text
hello
world
lines: 2
```

---

## 8) Exception Handling

### Example 1: try/except
```python
# Example: handle division by zero
try:
    x = 10 / 0  # will raise ZeroDivisionError
except ZeroDivisionError:
    print("Cannot divide by zero")
```
**Sample output**
```text
Cannot divide by zero
```

### Example 2: raise + custom exception
```python
# Example: validate input and raise an error
def set_age(age):
    if age < 0:
        raise ValueError("age must be non-negative")
    return age

try:
    print(set_age(-1))
except ValueError as e:
    print("Error:", e)
```
**Sample output**
```text
Error: age must be non-negative
```

---

## 9) Modules & Packages

### Example 1: built-in modules (os, sys)
```python
# Example: use built-in modules
import os
import sys

print("python:", sys.version.split()[0])   # show python version
print("cwd:", os.getcwd())                 # current directory
```
**Sample output**
```text
python: 3.x.x
cwd: /your/current/path
```

### Example 2: math module
```python
# Example: use math module
import math

print(math.sqrt(81))       # square root
print(math.ceil(2.2))      # round up
```
**Sample output**
```text
9.0
3
```

---

## 10) OOP (Object-Oriented Programming)

### Example 1: class and object
```python
# Example: a simple class
class User:
    def __init__(self, name):
        # store name in the object
        self.name = name

    def greet(self):
        # method uses self.name
        return f"Hello, {self.name}"

u = User("Karthikeya")
print(u.greet())
```
**Sample output**
```text
Hello, Karthikeya
```

### Example 2: inheritance
```python
# Example: inheritance
class Animal:
    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        # override parent method
        return "woof"

d = Dog()
print(d.speak())
```
**Sample output**
```text
woof
```

---

## 11) Advanced Python

### Example 1: list comprehension
```python
# Example: generate squares of even numbers
nums = [1, 2, 3, 4, 5, 6]
squares = [n * n for n in nums if n % 2 == 0]  # filter + map in one line
print(squares)
```
**Sample output**
```text
[4, 16, 36]
```

### Example 2: generator with yield
```python
# Example: generator yields values one by one (memory efficient)
def count_up_to(n):
    i = 1
    while i <= n:
        yield i          # pause and return i
        i += 1

for v in count_up_to(3):
    print(v)
```
**Sample output**
```text
1
2
3
```

---

## 12) Data Handling Libraries

### Example 1: NumPy basics
```python
# Example: NumPy array operations
import numpy as np

arr = np.array([1, 2, 3])
print(arr * 2)  # element-wise multiply
```
**Sample output**
```text
[2 4 6]
```

### Example 2: Pandas DataFrame basics
```python
# Example: create a DataFrame and compute a column
import pandas as pd

df = pd.DataFrame({"city": ["Hyd", "Mum"], "value": [10, 20]})
df["double"] = df["value"] * 2  # vectorized operation
print(df)
```
**Sample output**
```text
  city  value  double
0  Hyd     10      20
1  Mum     20      40
```

---

## 13) Automation & DevOps Python

### Example 1: run a shell command (subprocess)
```python
# Example: run a command and capture output
import subprocess

# Run 'echo' and capture stdout as text
result = subprocess.run(["echo", "hello"], capture_output=True, text=True, check=True)
print(result.stdout.strip())
```
**Sample output**
```text
hello
```

### Example 2: JSON handling
```python
# Example: parse and generate JSON
import json

payload = '{"env": "prod", "region": "europe-west2"}'
data = json.loads(payload)         # JSON string -> dict
data["owner"] = "devops"
print(json.dumps(data, indent=2))  # dict -> JSON string
```
**Sample output**
```json
{
  "env": "prod",
  "region": "europe-west2",
  "owner": "devops"
}
```

---

## 14) Cloud & Infrastructure Python

### Example 1: read env vars (common in cloud)
```python
# Example: read environment variables (like credentials path)
import os

# Get env var safely with default
project = os.getenv("PROJECT_ID", "demo-project")
print("project:", project)
```
**Sample output**
```text
project: demo-project
```

### Example 2: simple HTTP call (requests)
```python
# Example: call a public API endpoint
import requests

resp = requests.get("https://httpbin.org/get", timeout=10)
print(resp.status_code)  # HTTP status
print("url" in resp.json())  # check key exists in JSON response
```
**Sample output**
```text
200
True
```

---

## 15) Web & API Development

### Example 1: minimal Flask API
```python
# Example: simple Flask app (run: python app.py)
from flask import Flask, jsonify

app = Flask(__name__)

@app.get("/health")
def health():
    # Return JSON response
    return jsonify(status="ok")

if __name__ == "__main__":
    app.run(port=5000)
```
**Sample output**
```text
# When you call: curl http://localhost:5000/health
{"status":"ok"}
```

### Example 2: minimal FastAPI endpoint
```python
# Example: FastAPI app (run: uvicorn app:app --reload)
from fastapi import FastAPI

app = FastAPI()

@app.get("/hello")
def hello():
    # Return a dict (FastAPI auto-converts to JSON)
    return {"msg": "hello"}
```
**Sample output**
```text
# When you call: curl http://localhost:8000/hello
{"msg":"hello"}
```

---

## 16) Multithreading & Parallelism

### Example 1: threading
```python
# Example: run two tasks in parallel using threads
import threading
import time

def work(name):
    # simulate work
    time.sleep(0.2)
    print("done:", name)

t1 = threading.Thread(target=work, args=("A",))
t2 = threading.Thread(target=work, args=("B",))

t1.start()
t2.start()
t1.join()
t2.join()
print("all done")
```
**Sample output**
```text
done: A
done: B
all done
```

### Example 2: asyncio
```python
# Example: async concurrency using asyncio
import asyncio

async def task(name):
    # await yields control back to event loop
    await asyncio.sleep(0.1)
    return f"ok:{name}"

async def main():
    results = await asyncio.gather(task("X"), task("Y"))
    print(results)

asyncio.run(main())
```
**Sample output**
```text
['ok:X', 'ok:Y']
```

---

## 17) Testing

### Example 1: unittest
```python
# Example: unittest (run: python -m unittest test_demo.py)
import unittest

def add(a, b):
    # simple addition
    return a + b

class TestAdd(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)

if __name__ == "__main__":
    unittest.main()
```
**Sample output**
```text
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

### Example 2: pytest style (simple)
```python
# Example: pytest test function (run: pytest -q)
def is_even(n):
    # return True if n divisible by 2
    return n % 2 == 0

def test_is_even():
    assert is_even(4) is True
    assert is_even(5) is False
```
**Sample output**
```text
2 passed in 0.0Xs
```

---

## 18) Packaging & Deployment

### Example 1: requirements.txt + install (concept)
```python
# Example: show how to pin dependencies (this is not executed as python code)
# requirements.txt
# requests==2.31.0
# flask==3.0.0
print("See requirements.txt example in comments")
```
**Sample output**
```text
See requirements.txt example in comments
```

### Example 2: simple CLI entrypoint pattern
```python
# Example: a simple CLI entrypoint program
import argparse

def main():
    # define CLI args
    p = argparse.ArgumentParser()
    p.add_argument("--name", default="World")
    args = p.parse_args()

    # print greeting using parsed args
    print(f"Hello, {args.name}!")

if __name__ == "__main__":
    main()
```
**Sample output**
```text
# python cli.py --name Ravi
Hello, Ravi!
```

---

## Interview Focus Quick Practice

### Example 1: dict + loop + condition
```python
# Example: count word frequencies
text = "spark spark hadoop gcp"
freq = {}

for w in text.split():
    # get current count (default 0), then add 1
    freq[w] = freq.get(w, 0) + 1

print(freq)
```
**Sample output**
```text
{'spark': 2, 'hadoop': 1, 'gcp': 1}
```

### Example 2: function + exception handling
```python
# Example: safe integer parsing
def to_int(s):
    try:
        # try converting to int
        return int(s)
    except ValueError:
        # return None if conversion fails
        return None

print(to_int("123"))
print(to_int("abc"))
```
**Sample output**
```text
123
None
```

---



