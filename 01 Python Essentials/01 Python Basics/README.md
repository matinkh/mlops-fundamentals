# 1. Python Essentials for MLOps

Here we talk about the following

* Variables and Types
* Python data structures
* Working with Python data structures

So, if you know these, feel free to skip to the next part.



## 1.2 Variables and Types

### Key Terms

* **Variable:** A named location in memory that stores a value.
* **Assignment:** The = operator assigns a value to a variable.
* **f-String:** Formatted string literals.
* **Integer:** Positive or negative whole number (no decimal point).
* **Float:** Real number (with decimal point).
* **Boolean:** A T/F value.
* **None:** Represents no value assigned.
* **If/Else:** A conditional block.
* **Exception:** Errors that disrupt normal program flow.
* **Try/Except:** Catch exceptions in the `except` block after first trying the code in the `try` block.



```python
try:
  # Some operation that may cause multiple exceptions. It's best to know where the error
  # is coming from.
  result = a / b
  if result == 0:
    raise NoValuePassedException
  return result
  except ZeroDivisonError:
    print("b cannot be zero")
    return 0
  except NoValuePassedException:
    print("a cannot be zero")
    return -1
```



## 1.2 Python Data Structures

### Key Terms

* **List:** An ordered collection of values enclosed in `[]`.
* **Index:** The numeric position of an item in a list. (starts from 0)
* **Iteration:** Repeated execution of code on successive list items.
* **Dictionary:** Unordered collection of key-value pairs denoted in `{}`.
* **Key:** Unique identifier of values in a dictionary.
* **Value:** Data associated with a given key in a dictionary.
* **Tuple:** Fixed-size, immutable ordred collection similar to a list, denoted with `()`.
* **Set:** Unordered collection of unique objects. (helper to remove duplicates)
* **Membership:** Ability to check if a value is contained in a collection (e.g., lists, dictionaries, ...)
* **Methods:** Built-in functions that allow data manipulations.

### Notes:

* Lists can contain _any_ data types

```pyth
my_list = [1, "two", False, 12.5]
```

* You cannot have a list or a dict (collections) as they Key for Dictionaries

```python
my_dict = {[1, 2]: "sth"}  # raises error
```

* Iterating over a dictionary; Python iterates over Keys by default

```python
for key in my_dict:
  print(my_dict[key])
```

* You need key and values in a dictionary? Use `.items()`

```python
for key, value in my_dict.items():
  print(f"{key}: {value}"")
```



## 1.3 Working with Data Structures

### Key Terms

* **Append:** Adds an item to the end of a list.
* **Insert:** Inserts an item at a specified index in a list.
* **Extend:** Appends all items from one list onto another.
* **Pop:** Removes and returns an item at a specified index.
* **Get:**: Safely gets a dictionary value; if the key is NOT found, the default value is returned.

