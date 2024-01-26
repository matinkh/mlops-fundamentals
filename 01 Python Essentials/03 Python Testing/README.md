# 3. Python Testing

In this part, we'll cover

* How to write unitt tests
* Pytest
* Test conventions
* Useful patterns in testing
* Testing failures

## 3.1 Introduction to Testing

### Key Terms

* **Testing:** Validating code behavior through automated scripts.
* **Unit Test:** Testing isolated chunks of code like functions or classes.
* **Test Function:** An isolated test wrapped in a Python function.
* **Test Class:** A class that contains related test methods.
* **Assertion:** Boolean checks in test code to verify values match expectations.
* **Fixture:** Shared test data or state managed by the testing framework.



### Testing Conventions

Python's unittest is the **standard library** for testing.

```python
import unittest

class TestExample(unittest.TestCase):
  def test_assertion(self):
    self.assertEqual(1, 1)
    
unittest.main(argv=[''], verbosity=2, exit=False)
```

```bash
$ python my_test.py
```



Or, we can use **pytest**. Why?

* Using `assert` is discouraged. We can ignore all the `assert` statements in the code by setting a flag before running our python code.
* **pytest** enforces those assert statements.



**Directory layout:**

* The top-level directory is named `tests`
* Files need to be pre-fixed with `test_`
* Test functions need to be prefixed with `test_`
* Test classes need to be prefixed with `Test`



### Testing with Pytest

```bash
$ source venv/bin/activate
(venv) $ pip install pytest

(venv) $ pytest
### Goes through "tests" directory and pickes files "test_*.py" for evaluating.
```



## 3.2 Writing Useful Tests

### Key Terms

* **Plain Asserts:** Basic assertion statements in Python used to verify values and results.
* **Test Classes:** Classes that contain multiple related test methods and setup/teardown logic.
* **Parametrize:** Pytest decorator to run a test multiple times with different arguments.
* **Setup Method:** Code that runs before each test method in a Test Class.
* **Teardown Method:** Code that runs after each test method in a Test Class.



This is how a Test Class looks like:

```python
class TestStrToInt:
  def setup(self):
    print("This is setup before each test")
    
  def teardown(self):
    print("This is teardown after each test")
    
  def setup_class(cls):
    print("This is setup before class instanciation")
    
  def teardown_class(cls):
    print("This is teardown after all tests")
    
  def test_rounds_down(self):
    result = str_to_int("1.99")
    expected = 2
    assert result == expected
```

What is the difference between **test functions** and **test classes**?

* You can group tests in test classes
* You can simply add logic before and after tests. in classes (in `setup` and `teardown`)



What if you want to test a function for multiple cases? You can do that through **parameterization**.

```python
@pytest.mark.parametrize('value', ['y', 'yes', ''])
def test_is_true(value):
  result = str_to_bool(value)
  assert result is True
```



## 3.3 Testing Failures

### Key Terms

* **Test Failure Output:** pytest results containing details on which tests failed and why.
* **PDB (Python Debugger):** Tool to debug Python code by stepping through execution.
* **Pytest Fixtures:** Shared test/state managed by Pytest.
* **Pytest plugins:** Extensions that provide added Pytest functionality.
* **Pytest Options:** Commaon line flags that control Pytest runner behavior.



**PDB** allows to execute tests line by line to see what fails:

```bash
(venv) $ pytest --pdb test_failure_output.py

# Press "l" to show the code
...
```



What is the benefit of using **PDB** instead of Python's standard library **unittest**?

* It doesn't require using class inheritance, making it easier to write tests
* It is a test runner as well as a test framework, although you aren't required to use the framework
* That it has rich error reporting, making it easier to debug failures