# Writing Effective tests
Created Saturday 15 September 2018

Here we will discuss the design principles and how to create tests that are re-usable & maintainable over time

Clean test code with variables
------------------------------

* Always keep readable tests
* Minimize lines of code 
* try to reuse as much code as possible


lets start by using variables and use functions


Page object pattern
-------------------
A class for each page in the app
Each page has 

* Selectors
* Methods


### Goals:
Seperation of the test and code
More maintainable test code

### Pages (classes to be created):

* Sign-up page
* Users page


Test Suite organization
-----------------------
Important to think about as Selenium test suite grow and scale

### Best Practices:

* Each test class has one focus
	* Currently have a test for sign up
	* Later we can have classes to Log in , create blog posts
* Group tests by feature
	* Have sub suited based on feature
	* Sub-suite for blog, account
* Documentation of test
	* README
	* Outline details about tests
	* Helps thosse unfamiliar with tests



The test pyramid
----------------

* Ideal way to structure tests
* Different levels of testing
	1. UI
	2. Integration
	3. Unit


**Unit Tests** is at the bottom of the pyramid. They just hit the server and test a single function thus run in seconds and should be more level of unit tests
**Integration Tests** involve testing multiple services, create their own data & run in the range of tens of seconds thus decent amount of integration test
**UI Tests **where selenium test belong, end-to end user workflows are tested, but very slow as they run on browser so these should be least amount of tests

### Takeaway:
Selenium tests are valueable but remember to consider other types of testing. Avoid having a test suite full of selenium tests

