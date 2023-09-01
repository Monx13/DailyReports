# *Daily Report Aug/25/2023*
 
- [*Daily Report Aug/25/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
---

## **STATUS**
- Video continuation 12 CREATE Users and ADD SECURITY to your PASSWORDS 🔒 in MongoDB (FullStack JavaScript Bootcamp).
- We create a relationship between our backend and the users. We will review some good practices when saving passwords in the database and add tests.

- We learn:
  - Encrypting our password with bcrypt
  - Adding tests to the endpoint of creating users
  - Refactor test helper code

## **BLOCKERS**
- I keep having problems with the hss key, I have to upload manual repositories.

- No problem with the course content.

## **NOTES**

### Encrypting our password with bcrypt
Encrypting passwords is an essential practice to protect sensitive user information in applications. While you mentioned "encrypting," it's important to clarify that passwords should not be encrypted, but rather hashed and salted. Hashing is a one-way function that transforms the password into a fixed-length string of characters, and salting involves adding a random value (salt) to the password before hashing to increase security.

One of the commonly used hashing algorithms for securely hashing passwords is bcrypt. Bcrypt automatically handles the salting process and includes a built-in work factor that makes it intentionally slow to compute, which helps defend against brute-force and rainbow table attacks.

Here's a general outline of how to use bcrypt to hash and store passwords securely in a hypothetical application:

1. **Choose a Hashing Library**: Make sure you have a library that supports bcrypt hashing. Common programming languages have libraries for this purpose, such as `bcrypt` for Node.js, `passlib` for Python, and `bcrypt` for Ruby.

2. **Hashing and Storing Passwords**:

   - **Registration**: When a user registers, follow these steps:
     - Generate a random salt.
     - Combine the salt and the user's password.
     - Hash the combined value using bcrypt.
     - Store the hashed password and the salt in your database associated with the user's account.

   - **Login**: When a user logs in, follow these steps:
     - Retrieve the hashed password and the salt from the database for the given username.
     - Combine the salt and the provided password during login.
     - Hash the combined value using bcrypt.
     - Compare the generated hash with the stored hash. If they match, the password is correct.

Here's a simplified example in Python using the `passlib` library:

```python
from passlib.hash import bcrypt_sha256

# Registration
def register_user(username, password):
    salt = bcrypt_sha256.using(rounds=12).gen_salt()
    hashed_password = bcrypt_sha256.using(salt=salt).hash(password)
    # Store username, hashed_password, and salt in the database

# Login
def login_user(username, password):
    # Retrieve hashed_password and salt from the database based on the username
    stored_hashed_password = ...
    stored_salt = ...
    
    generated_hash = bcrypt_sha256.using(salt=stored_salt).hash(password)
    
    if generated_hash == stored_hashed_password:
        print("Login successful")
    else:
        print("Login failed")
```



### Adding tests to the endpoint of creating users
Adding tests to the endpoint for creating users is an essential part of maintaining the quality and reliability of your application. Testing helps ensure that the functionality of your endpoint is working as expected and that any future changes or updates don't inadvertently break existing functionality. Here's a general outline of how you can add tests to the endpoint responsible for creating users:

1. **Choose a Testing Framework**: Depending on the programming language and framework you're using, there are various testing frameworks available. Common choices include `unittest` for Python, `Jest` for JavaScript (Node.js), and `RSpec` for Ruby on Rails.

2. **Write Test Cases**:

   - **Positive Test Cases**: These test cases should cover the expected and correct behavior of your endpoint. For creating users, this could include:
     - Providing valid input data (username, password, etc.).
     - Ensuring the user is successfully created.
     - Verifying that the appropriate response is returned (e.g., a success status code).

   - **Negative Test Cases**: These test cases should cover scenarios where things might go wrong or where invalid input is provided. Examples include:
     - Providing duplicate usernames.
     - Providing invalid passwords.
     - Sending incomplete or missing data.
     - Ensuring the correct error responses are returned.

3. **Setup and Teardown**: Most testing frameworks provide ways to set up and tear down the environment before and after each test. In the context of creating users, this might involve creating a test database or clearing existing user data before each test case.

4. **Mocking and Dependency Injection**: If your endpoint interacts with external services or components, consider using mocks or dependency injection to isolate your tests and make them more focused on the endpoint's behavior.

5. **Assertions**: Use assertions to validate the expected outcomes of your tests. For instance, you can assert that a user was successfully created, that the response contains the expected data, or that the appropriate error response is received for invalid inputs.

6. **Running Tests**: Use the testing framework's tools to run your tests automatically. This could be as simple as running a command in your terminal.

Here's a simplified example of testing the user creation endpoint using Python's `unittest` framework:

```python
import unittest
from your_app import app, create_user

class TestUserCreation(unittest.TestCase):

    def setUp(self):
        self.app = app.test_client()

    def test_create_user_success(self):
        response = self.app.post('/create_user', json={'username': 'testuser', 'password': 'securepassword'})
        self.assertEqual(response.status_code, 201)  # Expecting a success status code
        # Add more assertions to validate the response or database state

    def test_create_user_duplicate_username(self):
        # Test the case where the username already exists
        response = self.app.post('/create_user', json={'username': 'testuser', 'password': 'password'})
        self.assertEqual(response.status_code, 400)  # Expecting a bad request status code
        # Add more assertions to validate the error response

if __name__ == '__main__':
    unittest.main()
```

### Refactor test helper code

Certainly, refactoring your test helper code can make your test suite more organized, maintainable, and readable. Here's an example of how you can refactor the test helper code for user creation tests using Python's `unittest` framework:

```python
import unittest
from your_app import app, create_user

class BaseTestCase(unittest.TestCase):
    def setUp(self):
        self.app = app.test_client()

class TestUserCreation(BaseTestCase):
    def test_create_user_success(self):
        response = self.app.post('/create_user', json={'username': 'testuser', 'password': 'securepassword'})
        self.assertEqual(response.status_code, 201)

    def test_create_user_duplicate_username(self):
        response = self.app.post('/create_user', json={'username': 'testuser', 'password': 'password'})
        self.assertEqual(response.status_code, 400)

if __name__ == '__main__':
    unittest.main()
```

In this refactored code:

1. The `BaseTestCase` class is introduced to provide a common setup for all test cases. It inherits from `unittest.TestCase` and sets up the test client from your app. This way, you don't have to repeat the setup code in each test case.

2. The `TestUserCreation` class now inherits from `BaseTestCase`. It contains the individual test methods for creating users.

This refactoring centralizes the setup logic and promotes cleaner code. You can further enhance this approach by:

- **Separating Test Data**: You might want to separate test data (input, expected output, etc.) from the test methods. This can be done by using class attributes or by creating separate modules/files for test data.

- **Using Fixtures**: Depending on your testing framework, you might use fixtures to set up common resources or to handle specific cases, making your tests more modular.

- **Mocking Dependencies**: If your code interacts with external services, using mocking libraries can help you isolate the tested functionality and control the behavior of external dependencies.

- **Custom Assertions**: If you have repetitive assertion patterns, consider creating custom assertion methods to enhance code reusability.

