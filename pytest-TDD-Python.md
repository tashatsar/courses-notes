# Unit testing with `pytest`🐍🚨
# 20.02.2023

## Some courses 💻📕🚀
- [Elegant Automation Frameworks with Python and Pytest course](https://www.udemy.com/course/elegant-automation-frameworks-with-python-and-pytest/):🐌🐌🐌
  - 👍Pro: tutor's language is pretty alive, with a nice sense of humor. Explanations are detailed, and the course has a lot of examples of code that are very easy to understand or reuse. I also liked the topics covered in the course👌 
  - 👎Cons: Some explanations can seem too long and too detailed, and the lecturer can step aside. Sometimes it can seem that it is not enough or not at all theoretical part, just examples. I used speed 2x, but desired would be around 3x🐌. The last update of the course was in June 2020👴
  - ⌚Duration: 6 hours 
- [Unit Testing and Test Driven Development in Python course](https://udemy.com/course/unit-testing-and-tdd-in-python):
  - 👍Pro: short course to get into the topic fast with many examples to start using immediately.
  - 👎Cons: sections about mocks and XUnit style are not detailed at all and provided too fast. 🚗💨 Code lacks explanations in general. Sometimes it's hard to follow the logic of the code.💩 ALso the course is pretty old and has not been updated since 2019. 👴
  - ⌚Duration: 2 hours 

## Tests, unit tests, TDD 🍎🍄
### Types of tests (according to [Atlassian](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing))
✨ **Unit testing**: testing functions and classes. The smallest unit of testing possible, module or component is tested in isolation. 

✨ **Integration testing**: testing how different modules or services work together. It is more expensive to run as it requires multiple parts.

✨ **Functional testing**: testing that output matches the business requirements.

✨ **End-to-end testing**: testing by replicating a user behavior in a complete application environment. Useful, but expensive to perform: the best would be to have a few key end-to-end tests and rely more on lower-level types of testing (unit and integration tests).

✨**Acceptance testing**: testing if the application satisfies end-user requirements and can be deployed. Can be made by testers as well as final users (alpha and beta testing).

✨ **Performance testing**: testing how a system performs under a particular workload. Measuring the reliability, speed, scalability, and responsiveness. 

✨ **Smoke testing**: testing the basic functionality of an application: meant to be quick to execute, checking that the major features of your system are working as expected.
  
### What is unit testing?
- Unit testing tests individual modules independently 🍎
- Unit tests are the first filter for catching bugs 🐛
- Tests should run fast with automated execution 🚀
- Unit testing is for the development environment rather than the production one 🔨

### What is test driven development (TDD)?
- Tests are written before the production code
- Tests and production code are written step by step
- The process is iterative: 🚨red phase, ✅green phase, 🔨refactor phase

🚨write a failing unit test -> ✅write prod code to pass only this test -> 🔨refactor test and code to make it clean -> 🚨write a new failing unit test -> ✅write prod code to pass only the new test -> 🔨refactor test and code to make it clean ->🚨-> ✅->🔨-> etc. until the feature is complete

#### Laws of TDD
Robert Martin created the following Laws of TDD in his book “Clean Code: A Handbook of Agile Software Development”:
1. You may not write any production code until you have written a failing unit test.
2. You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You may not write more production code than is sufficient to pass the currently failing unit test

## `pytest`📦
`pytest` is a [framework for tests](https://docs.pytest.org/en/7.2.x/). It uses standard Python assert statement 🐍
- **tests** are Python functions with "test" at the beginning of the function name: `test_pipeline_step`, `test_sum`. Tests can be grouped by putting them in the same module or class.
- **test class** should have "Test" at the beginning of the class name: `TestClass`, `TestSimilarThings`. Test class should NOT have `__init__` method.
- **filenames** for test modules should have "test" at the beginning or end of the filename: `test_*.py` or `*_test.py`.

BTW, the naming rules described above can be changed if needed. For doing so create a file named `pytest.ini` in the directory with the tests. Let's suppose we want to replace the word "test" for test functions with the word "check", so the content of the `pytest.ini` would be the following:
```
[pytest]
python_files = test_*
python_classes = *Tests
python_functions = check_*
```

### Install `pytest`🧰📦

`pip install pytest`: requires Python 3.7+.

Install some of the plugins:
- `pip install pytest-cov`: coverage reporting, produces coverage reports
- `pip install pytest-html`: generates an HTML report for test results
- `pip install pytest-xdist`: allows distributed execution modes (parallel test execution). Tests have to be isolated, otherwise doesn't make sense :melting_face:

### Run `pytest` with command line arguments
Run from the directory with tests: 
`python -m pytest`
for running all tests in all modules from the current working directory (pay attention to [naming](#pytest)). With command line arguments (all params [here](https://docs.pytest.org/en/7.1.x/reference/reference.html#command-line-flags)):
- `python -m pytest -v`: verbose mode
- `python -m pytest -q`: quiet mode (when running hundreds of tests)
- `python -m pytest -s`: show print statements on the console, don't capture the console output

Command line arguments for `pytest-cov` plugin (more params [here](https://pytest-cov.readthedocs.io/en/latest/config.html)): 
- `python -m pytest --cov-report=term`: generate coverage report in terminal
- `python -m pytest --cov-report=html`: generate coverage report as HTML

Command line for `pytest-html` plugin:
- `python -m pytest --html="results.html"`: generate HTML report what is called "results.html"

Command line for `pytest-html` plugin:
- `python -m pytest -n4`: run test using 4 treads. n3 is for 3 threads, etc. `-nauto` is supported. 

With several arguments: `python -m pytest -s -v`

### `pytest` decorators 🌺📦
- **`@pytest.fixture`**: need to use the same parameter for several tests? The fixture will be executed before the test!
```py
@pytest.fixture()
def import_package():
  import packages.package as package 
  return package
  
def test_module_1_exsists(import_package):
  assert (hasattr(import_package, 'module_1'))
  
def test_module_2_exsists(import_package):
  assert (hasattr(import_package, 'module_2'))
  
def test_no_fixture():
  assert smth
```

- **`@pytest.mark.parametrize`**: need to use different parameter sin the same test? 
Don't use loops, use parametrization!

```py
@pytest.mark.parametrize("our_params", ["param_value_1", "param_value_2", "param_value_3"])
def test_with_params(our_params):
  assert our_params
```
- **`@pytest.mark`**: need to create groups of tests to be run without other tests? Just mark your tests!
```py 
@pytest.mark.feature_a
def test_1_about_feature_A():
  assert smth

@pytest.mark.feature_a
def test_2_about_feature_A():
  assert smth

@pytest.mark.feature_a  
def test_1_about_feature_B():
  assert smth
  
def test_1_about_feature_C():
  assert smth

```
To launch only `test_1_about_feature_A` and `test_2_about_feature_A` run in the command line `python -m pytest -m feature_a`. In case you have to run several tests by how they are marked, use `python -m pytest -m "feature_a or feature_b"` (for tests that are marked with at least one of decorators) and `python -m pytest -m "feature_a or feature_b"`(for tests that are marked with both at the same time). Those code markers can be described in the `pytest.ini` file. The description is highly recommended for better code readability. For example:
```
[pytest]
python_files = test_*
python_classes = *Tests
python_functions = test_*

markers =
  feature_a: All tests for feature A testing 
```
 
- **`@pytest.mark.skip`**: need to skip a test? 
Test `test_to_skip` won't be executed!

```py
def test():
  assert something
  
@pytest.mark.skip  
def test_to_skip():
  assert smth
```
