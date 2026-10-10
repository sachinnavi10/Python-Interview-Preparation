# Day 3 – Python Interview Preparation

## 1. What is the difference between local and global variables in Python?

A **local variable** is created inside a function and can normally be used only within that function. A **global variable** is defined outside functions and can be read throughout the module.

To reassign a global variable inside a function, declare it with the `global` keyword. Without that declaration, an assignment creates or updates a local variable instead.

```python
message = "Hello"  # Global variable

def greet():
    name = "Asha"  # Local variable
    print(message, name)

greet()  # Hello Asha
```

Reassigning a global variable:

```python
count = 0

def increment():
    global count
    count += 1

increment()
print(count)  # 1
```

Use global variables sparingly; passing values into functions and returning results usually makes code easier to test and maintain.

## 2. What is the difference between positional, keyword, and default arguments?

- **Positional arguments** are matched to parameters by their order.
- **Keyword arguments** are matched by parameter name, so their order can vary.
- **Default arguments** have a value specified in the function definition. The default is used when the caller omits that argument.

```python
def describe_person(name, age=30):
    print(f"{name} is {age} years old.")

describe_person("Maya", 25)       # Positional arguments
describe_person(age=25, name="Maya")  # Keyword arguments
describe_person("Maya")           # Uses the default age: 30
```

Parameters with defaults must come after parameters without defaults:

```python
def connect(host, port=5432):
    print(f"Connecting to {host}:{port}")

connect("localhost")       # Connecting to localhost:5432
connect("localhost", 3306) # Connecting to localhost:3306
```

## 3. What are `*args` and `**kwargs`, and when do we use them?

`*args` collects any extra positional arguments into a **tuple**. `**kwargs` collects any extra keyword arguments into a **dictionary**. They are useful when a function needs to accept a flexible number of arguments.

```python
def show_items(*args):
    for item in args:
        print(item)

show_items("apple", "banana", "orange")
```

```python
def show_settings(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

show_settings(theme="dark", notifications=True)
```

You can use both together. The usual parameter order is regular parameters, `*args`, then `**kwargs`:

```python
def log_event(event, *details, **metadata):
    print("Event:", event)
    print("Details:", details)
    print("Metadata:", metadata)

log_event("login", "successful", user_id=42, source="web")
```

Here, `details` is `("successful",)` and `metadata` is `{"user_id": 42, "source": "web"}`.

## 4. What is the difference between `return` and `print()` in Python?

`print()` displays a value in the output (such as the console). `return` sends a value back from a function so the caller can store it, use it in another expression, or return it from another function.

```python
def add_and_print(a, b):
    print(a + b)

def add_and_return(a, b):
    return a + b

result = add_and_print(2, 3)  # Displays 5
print(result)                 # None: the function did not return a value

total = add_and_return(2, 3)
print(total)                  # 5
print(total * 2)              # 10: the returned value can be reused
```

If a function reaches its end without a `return` statement, Python returns `None`.

## 5. What is a lambda function in Python, and how is it different from a normal function?

A **lambda function** is a small anonymous function written with the `lambda` keyword. It can contain only one expression, and that expression's result is returned automatically. It is often used for a short operation passed to another function.

```python
square = lambda number: number * number
print(square(4))  # 16
```

The same operation as a regular function:

```python
def square(number):
    return number * number
```

For example, a lambda can provide a sorting key:

```python
students = [("Asha", 88), ("Ravi", 95), ("Maya", 91)]
students_by_score = sorted(students, key=lambda student: student[1])
print(students_by_score)
# [('Asha', 88), ('Maya', 91), ('Ravi', 95)]
```

Use a lambda for a simple one-expression function. Use `def` when the logic needs multiple statements, a descriptive function name, or documentation.