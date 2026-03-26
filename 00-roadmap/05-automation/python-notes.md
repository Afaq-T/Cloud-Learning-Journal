# Python Fundamentals Notes — Week 5 Monday

---

## Why Python for Cloud Engineers?

Python is now expected at entry-level cloud positions. You do not need to become a developer. You need enough to write a 30-line automation script and understand what Python code does when you read it.

---

## Variables

A variable stores data in memory. You give it a name and assign a value using `=`.

```python
name = "Afaq"
city = "Rawalpindi"
age = 21
is_student = True
```

Rules:
- Cannot start with a number
- No spaces — use underscore: `my_variable`
- Case sensitive — `Name` and `name` are different

---

## Data Types

| Type | Example | What it stores |
|---|---|---|
| `str` | `"Hello"` | Text |
| `int` | `42` | Whole number |
| `float` | `3.14` | Decimal number |
| `bool` | `True` / `False` | True or False |
| `list` | `["East US", "West EU"]` | Ordered collection |
| `dict` | `{"name": "VM1", "status": "Running"}` | Key-value pairs |

Check data type: `print(type(name))`

---

## print() and f-strings

```python
print("Hello World")
print(name)
print(f"My name is {name} and I live in {city}")
```

f-strings use `f` before the quote and `{}` around variable names. This is the standard in modern Python.

---

## if / else Conditions

Runs different code depending on whether a condition is True or False.

```python
status = "Running"

if status == "Running":
    print("VM is healthy")
elif status == "Stopped":
    print("Warning: VM is stopped")
else:
    print("Unknown status")
```

**Indentation is critical.** Code inside if/else must be indented 4 spaces. Wrong indentation = error.

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |

---

## for Loops

Repeats code for each item in a collection.

```python
regions = ["East US", "West Europe", "Southeast Asia"]

for region in regions:
    print(region)
```

With position number:
```python
for i, region in enumerate(regions, 1):
    print(f"{i}. {region}")
```

Through a dictionary:
```python
for key, value in vm.items():
    print(f"{key}: {value}")
```

`range(3)` generates `0, 1, 2` — not 1, 2, 3.

---

## Functions (def)

A reusable block of code. Define once, call many times.

```python
def check_status(status):
    if status == "Running":
        print("VM is healthy")
    elif status == "Stopped":
        print("Warning: VM is stopped")
    else:
        print("Unknown status")

check_status("Running")
check_status("Stopped")
```

With return value:
```python
def get_greeting(name):
    return f"Hello, {name}!"

message = get_greeting("Afaq")
print(message)
```

Rules:
- `def` keyword starts the definition
- Body must be indented
- `return` sends a value back to the caller
- Define before you call

---

## Lists

Ordered collection — items stay in order.

```python
regions = ["East US", "West Europe", "Southeast Asia"]

regions.append("UAE North")       # Add item
regions.remove("West Europe")     # Remove item
print(regions[0])                 # Access by index (starts at 0)
print(len(regions))               # Length
if "East US" in regions:          # Check if exists
    print("Found")
```

---

## Dictionaries

Key-value pairs — look up a key to get its value.

```python
vm = {
    "name": "vm-prod-01",
    "region": "East US",
    "status": "Running",
    "cpu_percent": 45
}

print(vm["name"])              # Access value
print(vm.get("status"))        # Safer access — returns None if key missing
vm["status"] = "Stopped"       # Update value
vm["os"] = "Windows Server"    # Add new key
```

---

## Reading Files

```python
with open("sample-log.txt", "r") as file:
    for line in file:
        if "ERROR" in line:
            print(f"ALERT: {line.strip()}")
```

`with open()` automatically closes the file. Always use this pattern.

---

## Common Errors

| Error | Cause | Fix |
|---|---|---|
| `IndentationError` | Wrong spacing | Use exactly 4 spaces |
| `NameError` | Variable not defined | Check spelling or define first |
| `KeyError` | Dictionary key missing | Use `.get()` instead of `[]` |
| `SyntaxError` | Typo in code | Check the line number in error |

---

## Practical Example — VM Health Checker

```python
vms = [
    {"name": "vm-web-01", "status": "Running", "cpu_percent": 92},
    {"name": "vm-app-01", "status": "Running", "cpu_percent": 35},
    {"name": "vm-db-01",  "status": "Stopped",  "cpu_percent": 0},
    {"name": "vm-dev-01", "status": "Running", "cpu_percent": 88},
    {"name": "vm-test-01","status": "Running", "cpu_percent": 12},
]

for vm in vms:
    if vm["status"] == "Running" and vm["cpu_percent"] > 80:
        print(f"WARNING: {vm['name']} — CPU at {vm['cpu_percent']}%")
    elif vm["status"] == "Running":
        print(f"OK: {vm['name']} — CPU at {vm['cpu_percent']}%")
    else:
        print(f"NOTICE: {vm['name']} is Stopped")
```

---

## Key Rules

- `=` assigns a value — `==` compares two values
- Lists use `[]` — Dictionaries use `{}`
- Indentation is not optional — it defines the structure
- f-strings are the cleanest way to combine text and variables
- `range(3)` gives `0, 1, 2` not `1, 2, 3`
