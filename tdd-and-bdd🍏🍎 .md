# Test and Behavior Driven Development🍏🍎

## Course [Test and Behavior Driven Development](https://www.coursera.org/learn/test-and-behavior-driven-development-tdd-bdd)💻📕🚀 

👍Pros: 

👎Cons:

⌚Duration: _ hours

💯Overall: _/10

## Intro to testing🍏 

Why to do testing:
- verification that the software works as expected
- preventing future code breaks and compatibility issues
- reducing overall development time

The software **testing process includes four levels**: 
1) unit: testing individual units or components of a software system
2) integration: combine individual units and test them as a group
3) system: test a complete, integrated system
4) acceptance: the system is tested for acceptability by the end user

Test cases **drive code design** in both behavior driven development (BDD) and test driven development (TDD). 

BDD: focuses on the system from the outside in, used for for integration and acceptance testing 

TDD: focuses on the system from the inside out, used for for unit testing

## Test driven development🚨✅🔨

In TDD, test cases drive code design. The Red🚨/Green✅/Refactor🔨 workflow.
TDD saves development time and ensures that the code works as expected. 

To create a DevOps pipeline, you must automate all testing. 

### Frameworks:
- The **xUnit series** is one of the most popular testing frameworks for TDD, while others include Jasmine for JavaScript, Mocha for Node.js, and SimpleTest for PHP
- The two most popular testing frameworks for Python are **PyUnit and Pytest**. Two other popular testing frameworks for Python are Doctest and RSpec
- **Nose** is a Python test runner that can add color to test output and call the code coverage tool

### Assertions and fixtures
**Assertions** are checks to determine if tests have passed or failed. To create assertions in Python, developers can use the assert () function or any additional PyUnit asserts.

Happy paths verify that a function returns positive outcomes when expected, while sad paths confirm that a function responds to exceptions appropriately and without breaking.

Test **fixtures** establish a known initial state before and after each test. Why test fixtures:
- loading a database with a known data set
- creating mock objects
- etc
  
Test fixtures operate at three levels of specificity: Module, Test case, Test

### Advanced Methods for Test Driven Development

**Test coverage:**
- the higher the test coverage, the more confidence that code works as expected
- missing test coverage reports help to identify lines of code that need test cases

**Factories and fakes** are useful for creating and maintaining a large amount of test data.
- **Factories** generate fakes with realistic test data.
- **Fakes** behave like real objects during testing

**Mocking**: creating objects that mimic the behavior of real objects in ways that you can control. Why? To isolate tests from a remote component or external system. **Patching** is a mocking technique by which developers change the behavior of a function call. Python’s mock library provides two patching techniques:
- Patching a function’s return value
- Replacing a function with another function (the side effect technique)


**Conclusion:
TDD keeps you focused on the application’s requirements before writing a single code line.
The TDD workflow is a back-and-forth process.**


## Behavior Driven Development 🥒 
In BDD, you test the system’s behavior from the outside in.
BDD ensures that the system behaves as intended. In the software testing process, the appropriate levels of performing BDD are integration, system, and acceptance testing.


In the BDD workflow:
1. create examples to describe the desired behavior
2. run those examples as automated tests
3. write additional tests as needed

The workflow leads to one document that acts as both the specification and the tests for your software. To create an example in Gherkin syntax, you break it down into steps using **Given, When, Then, And, and But keywords.**
