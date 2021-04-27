# planitassessment
# Selenium Python testing

This readme for how the input values(valid/invalid) are validated in the contact form
and add items to the shopping cart and verify them.

# Installation  requirements
Below softwares are required to create and execute the test cases

1.Download selenium

2.Download chromedriver

3.Download python latest version

4.Download pycharm latest version community edition


# Create a python project
1.To create a python project 

2.Goto file menu and click on create a new project

3.Once the project is cerated create a python file such as test_planit.py file in this case


# Selenium and Python 
1.Once the python file is created 

2.Install the packages required to run selenium inside python

3.Install the below packages for using selenium with python. All packages were downloaded using Pycharm 

from selenium import webdriver

from selenium.webdriver.common.alert import Alert

from selenium.webdriver.common.by import By

from selenium.webdriver.support import expected_conditions as EC

from selenium.webdriver.support.ui import WebDriverWait

import actions

from selenium.webdriver import ActionChains

import unittest

import assertion


# How to install packages using Pycharm
1.Goto File in the Menu

2.Goto Settings

3.Choose the project you want the packages to be installed for

4.Click on the Python interpreter

5.Choose the plus sign and in the serach bar write the name of the package you want to install such as assertion

6.Click on Install on the bottom

7.Once a package is installed you will get a success message that your package is installed

8.Once you have all the required packages installed import them your project's python file


# Start writing the code
1.The code starts with creating a class class PythonOrgSearch(unittest.TestCase):

2.Once this class is created various functions can be written to complete the testing

3.The first task is to setup the driver to run a browser in selenium

4.All the functions representing the test cases in should start with keyword test_ such as "def test_<test_case_name>:

# Demo code for setting up the driver 
User can use any browser for testing 
In this case, Pyhton uses chromedriver to run the browser
download the chrome browser on your local machine and give the path of your local directory where the chrome driver is saved:
for example - C:\Users\<yourusername>\Downloads\chromedriver_win32\chromedriver.exe

self.driver = webdriver.Chrome(r"C:\Users\kgaur\Downloads\chromedriver_win32\chromedriver.exe")  

  
  
# First Test case to validate the validation messages in the contact page and then enter the valid input values in them and again validate the fields 
1.Requires below steps to follow:

2.Call the contact page 

3.Click the submit button on this page

4.Get all the validation error messages

5.Validate the error messages

6.Enter the valid values in the fields mandatory ones

7.Check if the validation messages disappear

# Demo code for first test case:
 def test_setUp(self):
  driver= self.driver
  self.driver.get("https://jupiter.cloud.planittesting.com/#/")
  contactus_btn = self.driver.find_element_by_xpath('//*[@id="nav-contact"]/a').click()
  self.driver.implicitly_wait(10)
  print("Submit button is clicked.")
  submit = self.driver.find_element_by_xpath("/html/body/div[2]/div/form/div/a").click()
  sucmsg = self.driver.find_element_by_xpath("/html/body/div[2]/div/div").text
  print("Validation message on top of the page" + sucmsg)
  self.assertEqual(sucmsg,'We welcome your feedback - but we won\'t get it unless you complete the form correctly.')
  forname = self.driver.find_element_by_xpath("//input[@id='forename']/following-sibling::span").text
  print("Validation message for forename:" + forname)
  self.assertEqual(forname,'Forename is required')
  email = self.driver.find_element_by_xpath("//input[@id='email']/following-sibling::span").text
  print("Validation message for Email:"+ email)
  self.assertEqual(email,'Email is required')
  message = self.driver.find_element_by_xpath("//textarea[@id='message']/following-sibling::span").text
  print("Validation message for Message:"+ message)
  self.assertEqual(message,'Message is required')
  print("Enter the valid values for mandatory fields")
  forename = self.driver.find_element_by_xpath('// *[@id = "forename"]').send_keys("test")
  email = self.driver.find_element_by_xpath('//*[@id="email"]').send_keys("test@test.com")
  msg = self.driver.find_element_by_xpath('//*[@id="message"]').send_keys("test msg")
  sucmsg = self.driver.find_element_by_xpath("/html/body/div[2]/div/div").text
  print("Validation message on top of the page " + sucmsg)
  self.assertEqual(sucmsg, 'We welcome your feedback - tell it how it is.')
  forname = self.driver.find_element_by_xpath("//*[@id='forename']").text
  print("Validation message for forename:" + forname)
  self.assertEqual(forname, '')
  help_email1 = self.driver.find_element_by_xpath("//input[@id='email']/following-sibling::span").text
  print(help_email1)
  self.assertEqual(help_email1, 'Your email address will only be used in reply to this message.')
  help_email2 = self.driver.find_element_by_xpath("//*[@id='email-group']/div/span[2]").text
  print(help_email2)
  self.assertEqual(help_email2, 'We never send spam email or give your email address to others.')
  message = self.driver.find_element_by_xpath("//textarea[@id='message']").text
  print("Validation message for Message:" + message)
  self.assertEqual(message, '')



# Second test case to validate the success message after entering the valid values in the contact us page for mandatory fields

1.Goto contact us page 

2.Enter valid values in the mandatory fields

3.Click on the Submit button

4.Wait for the success message to appear

5.Validate the success message

# Demo code for second test case:
 def test_validCase(self):
        driver = self.driver
        self.driver.get("https://jupiter.cloud.planittesting.com/#/")
        contactus_btn = self.driver.find_element_by_xpath('//*[@id="nav-contact"]/a').click()
        self.driver.implicitly_wait(10)
        # Insert valid values for all mandatory fields
        print("Enter valid values in all mandatory fields")
        forename = self.driver.find_element_by_xpath('// *[ @ id = "forename"]').send_keys("test")
        email = self.driver.find_element_by_xpath('//*[@id="email"]').send_keys("test@test.com")
        msg = self.driver.find_element_by_xpath('//*[@id="message"]').send_keys("test msg")
        # Submit all the mandatory web elements with valid input values
        submit = self.driver.find_element_by_xpath("/html/body/div[2]/div/form/div/a").click()
        # Get the success message after submission
        print("Validate the success message")
        msg_text2 = driver.find_element_by_xpath("//*[@class = 'alert alert-success']").text
        # Wait for the web element to appear
        self.driver.implicitly_wait(10)
        print(msg_text2)
        # Test the success message against the expected success message
        self.assertEqual(msg_text2,'Thanks test, we appreciate your feedback.')

#Third test case to enter invalid values in the contact us page and validate the message
1.Checked which fields have a validation such as email

2.Forename and message although mandatory fields have no validation messages associated with then other than the mandatory field

3.Test the email and the message appearing due to entering invalid email in the email field
validate both the messages

# Demo code for third test case:
 def test_invalidData(self):
          driver=self.driver
          self.driver.get("https://jupiter.cloud.planittesting.com/#/")
          contactus_btn = self.driver.find_element_by_xpath('//*[@id="nav-contact"]/a').click()
          self.driver.implicitly_wait(10)
    # Out of three mandatory field the validation is set onto email field
          print("enter the invalid value in the Email field")
          email = self.driver.find_element_by_xpath('//*[@id="email"]').send_keys("a")
          txt_email = self.driver.find_element_by_xpath("//input[@id='email']/following-sibling::span").text
          print(txt_email)
    # Test the validation message for the email field for an invalid input value
          self.assertEqual(txt_email,'Please enter a valid email')
          sucmsg = self.driver.find_element_by_xpath("/html/body/div[2]/div/div").text
          print("Validate the error message on top of webpage" + sucmsg)
    # Validate the message on top of the web page for invalid entry into the email field
          self.assertEqual(sucmsg,'We welcome your feedback - but we won\'t get it unless you complete the form correctly.')


# Fourth test case to add items in the shopping cart and verify them
1.Goto shopping page

2.Select two quantity of the first item and one quantity for the second item

3.Add them to the shopping cart

4.Once added verify their presence and details associated with the items

# Demo code for fourth test case:
 def test_addToCart(self):
      driver = self.driver
      self.driver.get("https://jupiter.cloud.planittesting.com/#/")
    # Get the URL for the Shop from the Menu
      shop = self.driver.find_element_by_xpath('//*[@id="nav-shop"]/a').click()
    # Add the first item Fluffy bunny from the given product list
      print("add items to the cart")
      driveButton = WebDriverWait(self.driver, 10).until(EC.presence_of_element_located((By.XPATH,"//h4[text()='Fluffy Bunny']/../p/a")))
      bunny = self.driver.find_element_by_xpath("//h4[text()='Fluffy Bunny']/../p/a")
      action = ActionChains(self.driver)
    # Double click function used to add two items on one click
      action.double_click(bunny).perform()
    # Add the second item Funny cow from the product list
      cow = self.driver.find_element_by_xpath("//h4[text()='Funny Cow']/../p/a")
      cow.click()
    # Click on the Cart
      cart = self.driver.find_element_by_xpath("//*[@id='nav-cart']/a").click()
    # Verify items in cart
      print("verify items in the cart")
      WebDriverWait(self.driver, 20).until(EC.presence_of_element_located((By.XPATH, "/html/body/div[2]/div/form/table/tbody/tr/td")))
    # Locate the cart
      table = self.driver.find_elements_by_xpath("/html/body/div[2]/div/form/table/tbody/tr/td")
    # Iterate over the items in the cart
      for i in table:
       print(i.text)


# Close the browser

1.Once all the test cases run quit the browser using a tearDown function

# Demo code to close the browser:
 def tearDown(self):
      driver=self.driver
      self.driver.quit()

# The last and the final task is to call the main class to run all the functions or test cases

# Demo code for the main class:

if __name__ == "__main__":
   unittest.main()
   
# Directory structure 
1. All the test file are stored under the test package 

2. In this case, the test package was created in the python project and inside this package a python file was created to run the test cases.

3. Directory structure:
seleniumproject -> test -> test_planit.py

# Final step to run the Python project or file using pycharm
1.Import the file into your directory 

2.Open pycharm

3.Open the python file in pycharm

4.In this case, Pyhton uses chromedriver to run the browser

5.Download the chrome browser on your local machine and give the path of your local directory where the chrome driver is saved:
for example - C:\Users\<yourusername>\Downloads\chromedriver_win32\chromedriver.exe

6.Right on the python file and click run 

7.Once the file will user can see test cases running one after another and finally four passed test cases
