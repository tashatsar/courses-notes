# Test and Behavior Driven Development🍏🍎

## Course [Test and Behavior Driven Development](https://www.coursera.org/learn/test-and-behavior-driven-development-tdd-bdd)💻📕🚀 

👍Pros: An incredible lively and engaged lecturer John Rofrano, a wide range of topics, a huge number of [examples](https://github.com/tashatsar/tdd-bdd-final-project) that can then be reused in real projects. I highly recommend it to everyone. 

👎Cons: uses unittest instead of pytest. The final project was a bit overwelming. The course really has a lot of material, and it's hard to grasp it all at once.

⌚Duration: 19 hours

💯Overall: 9/10

The link contains many practical examples, united into a single project: https://github.com/tashatsar/tdd-bdd-final-project 

## Table of Contents
1. [Intro to testing🍏](#intro-to-testing)
2. [Test driven development🚨✅🔨](#test-driven-development)
	- [Frameworks](#frameworks)
	- [Assertions and fixtures](#assertions-and-fixtures)
	- [Advanced Methods: coverage, fakes, mocking](#advanced-methods-for-tdd)
3. [Behavior Driven Development](#behavior-driven-development)
4. [Course Summary](#course-summary)


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

### Advanced Methods for TDD🤓🤥

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


## Behavior Driven Development🥒🎠
In BDD, you test the system’s behavior from the outside in.
BDD ensures that the system behaves as intended. In the software testing process, the appropriate levels of performing BDD are 
- integration
- system
- acceptance testing

In the **BDD workflow:**
1. create examples to describe the desired behavior
2. run those examples as automated tests
3. write additional tests as needed

The BDD workflow leads to one document that acts as both the specification and the tests for your software.

The workflow leads to one document that acts as both the specification and the tests for your software. To create an example in Gherkin syntax, you break it down into steps using **Given, When, Then, And, and But keywords.**

**BDD tools**: Cucumber and Behave (both use the Gherkin syntax), Concordion

### Running Behave 🎠

Behave uses Gherkin syntax. Gherkin is used for writing behavior specifications. The main keywords:
- **Feature**: Describes a feature of the application. Represent user stories and are described using the syntax: “As a [role], I want [functionality], So that [benefit].” Each feature can be placed in its own specification file.
- **Scenario**: Represents a specific situation or example of how the feature should behave. Describe specific behaviors of a feature using the Given, When, Then syntax. Each scenario serves as a complete test case.
- **Given**: Sets up the initial context or state before the action occurs.
- **When**: Describes the action or event that triggers the behavior.
- **Then**: Specifies the expected outcome or result after the action.
- **And**: Used to add additional conditions or actions to the Given, When, or Then steps.
- **But**: Similar to And, but typically used to introduce a contrasting condition.

📁 Features folder for feature files and a Steps folder for Python steps files.

**Behave actions when run:**
1. reads the Gherkin statements in each feature file
2. looks for matching Python steps in the steps files
3. executes the test functions embedded within the Python steps

**Behave environment:**
1. import getenv() and other required modules.
2. declare global variables from the environment.
3. define your test fixtures.

Behave reports all missing Python steps and suggests code snippets that you can use for them.

The **workflow for implementing Python steps** is as follows:
1. Implement a step
2. Run Behave and ensure the step passes
3. Implement the next step that fails
4. Run Behave and ensure that this step passes
5. Repeat this process until all steps pass

Context is a variable that gets passed into every step definition. To pass information between steps, store it in the context variable of one step and call on that variable in another step. Variable substitution reduces the steps needed and maximizes reuse.

To substitute variables, you follow this process:
1. Replace data in the decorator string with variables enclosed by curly braces.
2. Add step implementation parameters with the same names as those variables.
3. Substitute those variable names instead of the strings passed in from the feature file.


## Course Summary📚

**Testing verifies that your software will work as expected when you or others use it.** The software testing process includes four **levels**: unit, integration, system, and acceptance. Test cases drive code design in both behavior driven development (BDD) and test driven development (TDD). **BDD** focuses on the system from the outside in, while **TDD** focuses on the system from the inside out.

The TDD Red/Green/Refactor **workflow** includes three steps:
1. Write a failing unit test case for the code you wish you had
2. Write enough code to pass this test case
3. Refactor the code to improve its quality

**Nose** is a Python test runner that can add color to test output and call the code coverage tool.

Test **fixtures** establish a known initial state before and after each test. **Factories and fakes** are useful for creating and maintaining large test data. **Patching** is a mocking technique by which developers change the behavior of a function call. **Mock objects** are objects that mimic the behavior of real objects in ways that you can control.

**Behavior driven development** (BDD) is a test-first approach to development that ensures that an application behaves as intended. In the software testing process, the appropriate levels for performing BDD are integration, system, and acceptance testing. The BDD workflow includes three steps:
1. Create examples or scenarios to describe the desired behavior
2. Run those examples as automated tests
3. Write additional tests as needed

To build a BDD specification, you write a feature and then write scenarios using the Given, When, Then syntax. Context is a variable that gets passed into every step definition. Variable substitution reduces the steps needed and maximizes reuse.

**TEST FIRST!**
