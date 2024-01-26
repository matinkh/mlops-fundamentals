# 2. Python Advanced

In this part, we'll cover

* Working with functions
* Classes and methods
* Modules and advanced usages

If you know these subjects, move on to the next part.



## 2.1 Working with Functions

### Key Terms

* **Function:** A reusable block of code that performs a specific task.
* **Arguments:** Values padded into a function.
* **Variable arguments:** Allows passing an arbitrary number of argumetns to a function.
* **Keyword arguments:** Arguments passed by name rather than position. Can have <u>default values</u>.



**Arguments**

```python
# Mandatory arguments
def squared(number):
  return number**2

# Optional arguments (keyword arguments)
def greetings(full_name="John Doe"):
  print("Greetings ", full_name)
```

**Variable arguments**

```python
# 0 or more arguments
def family_members(*args):
  for name in args:
    print(name)
    
# 0 or more keyword arguments
def stats(**kwargs):
  for key, value in kwargs.items():
    print(f"{key} --> {value}"")
```

* `**kwargs` internally becomes a dictionary.



## 2.2 Building Classes and Methods

### Key Terms

* **Class:** Blueprint for creating objects.
* **Instance:** Object that is created from a class.
* **Method:** Function that belongs to a class.
* **Constructor:** Special method that runs when an instance is created.
* **Inheritance:** Creating a child class from parent class. It inherits attributes and methods.

```python
# Class definition
class DataReader:
  # Constructor
  def __init__(self, db_connector):
    self.db_connector = db_connector
  
  # Method
  def read_db_data(self, query: str):
    return self.db_connector.read(query)
  
# Instance
data_reader = DataReader(MySqlDbConnector())

for employee_data in data_reader.read_db_data("SELECT * FROM Employees"):
  print(employee_data)
```



## 2.3 Modules and Advanced Usage

### Key Terms

* **Module:** A python file containing reusable code like functions or classes.
* **Import:** Retrieves modules making their contents available in current namespace.
* **Virtualenv:** Self-contained directory housing isolated Python packages.
* **Activation:** Configures shell to use _virtualenv_'s dedicated Python interpreter.
* **Pip:** Python tool for installing/managing packages and dependencies.



**Module:** Python modules are `.py` files.

```
utility
 |--- __init__.py
 |--- db_connector.py
```

We can **import** modules like:

```python
from utility.db_connector import DbConnector

def MyClass:
  def __init__(self, db_connector: DbConnector):
    self.db_connector = db_connector
```

A **Python script** looks like this: (it's defined by `__name__ == "__main__"`)

```python
import sys

def main(args):
  for arg in args:
    print(arg)
    
if __name__ == "__main__":
  main(sys.argv)
```

We can **call** a script like:

```bash
$ python my_script.py
```

To create a **virtual environment**:

```bask
# Create a virtualenv
$ python -m venv venv

# Activate virtualenv
$ source venv/bin/activate
$ which python
>>> venv/bin

# Install packages
$ (venv) pip install pandas

# Deactivate
$ (venv) deactivate
```

