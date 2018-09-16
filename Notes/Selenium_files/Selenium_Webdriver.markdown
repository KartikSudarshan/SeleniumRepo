# Selenium Webdriver
Created Saturday 15 September 2018

Using the Selenium WebDriver
----------------------------

### Goals of Web Driver:

* Quickly and easily write automated tests
* Maintain a standardized API that is user friendly
* Emulate actions of users

Thus writing test with webdriver is now straight forward

### Ideal for users of WebDriver:

* Testers who want to save time manually testing
* Developers have confidence in testing to know they aren't introducing regressions
* To Test accross multiple browsers and platforms
* A customizable and powerful framework


### WebDriver architecture :
Testscripts ↔ WebDriver API ↔ Browser

#### Language support:

* C,
* Java, 
* Ruby, 
* Python, 
* JavaScript


#### Platform Support

* Windows
* MacOS
* Linux


#### Browser support

* Chrome
* Firefox
* IE
* Safari


### Browser Driver:

* One for each of the major browsers
* Each has its own API maintained by browser vendor
* Drivers implemented in same language as the browser


Using the API
-------------
Look in the ruby documentation of web driver to familiarize with classes and methods available


##### Sample script
The Driver opens a new firefox browser, navigates to google.com types in search box and clicks on search button
	require "selenium-webdriver"

How to setup the driver needs to be specified (may require details like browser name, version, resolution)
``driver = Selenium::WebDriver.for :firefox``
``driver.navigate.to "http://google.com"``

After creating the driver we need to search for elements in the webage before interacting with them. So find an element
Different locator variations are present, but rule of thumb is to stick to 1 locator 

``element = driver.find_element(name: 'q')``
``element.click``
``element.send_keys "Hello WebDriver!"``
``element.submit``

Close the driver session
``driver.quit``

Write a test
------------

### Break Down the process into steps:

1. **Decide what to automate:** requires the knowledge of the application under test
2. **Outline the test scenarios:** think about inputs and outputs & Determine the value of each scenario
3. **Find the web elements needed for testing:** Need to locate all elements used in the tests


Sample rails blog application.
Once this is done we need to add assertions

Add structure to test
---------------------
Once this is done we need to add assertions
In the Sample rails blog application, to confim that a user is signed up we now need to add a final step in the test to verify this

Running Tests
-------------
Best to run a test often for CI/CD reasons.
rspec blog-test.rb

All about the driver
--------------------
An advantage of the webdriver is that it suports runnning tests in all major browsers, Check in Seleniumhq for complete list

### Similarities
Currently the browsers corresponding webdriver was required for running the test so if different browser is required then we need to do setup for that browser
Other similarities are the API Functionality & part of the W3C spec standard

### Differences

* Speed varies between different browsers
* Might differ slightly in syntax or functionality
* Documentation details may vary


#### ChromeDriver

* Maintained by Google
* implements the webdriver wire protocol for chromium
* Available on android and desktop


#### geckodriver

* Owned by Mozilla 
* written in rust (Mozilla's ope source systems programming language)
* Default for Firefox since selenium 3.0 and support is best for firefox 55+


#### EdgeDriver

* Maintained by Microsoft
* Written in C#
* support is best in windows 10


#### Safari Driver

* Maintained by Apple
* SafariDriver included by default
* Built with Webkit (open-source web browser and application  engine)


Refer to the usage data to determine the most commomly used browsers

