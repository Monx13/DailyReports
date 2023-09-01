# *Daily Report Aug/23/2023*
 
- [*Daily Report Aug/23/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
---

## **STATUS**
- Video 11 🔴 Backend Testing with Express using Jest and SuperTes ~ Fullstack Bootcamp Javascript was seen.

- Video 11 continues with the practice of video 10.

- We learn:
  - How to use environment variables in Windows with Cross-ENV.
  - How to use SuperTest for Express Testing.
  - Make the tests in Jest
  - How to jump tests that do not interest that they run.
  - Avoid depending on Side Effects in your tests.
  - Among other good practices.

- A new Part 4 folder is created in the repository. [Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)


[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)

[Fullstack Bootcamp Course](https://fullstackopen.com/es/)

## **BLOCKERS**
- None

## **NOTES**

### How to use environment variables in Windows with Cross-ENV.

`cross-env` is a popular npm package that allows you to set environment variables in a cross-platform manner, including Windows. It's commonly used in Node.js projects to manage environment variables during the build or execution process. Here's how you can use `cross-env` to set and use environment variables in Windows:

1. **Install cross-env:**
   
   First, make sure you have Node.js and npm installed. If not, download and install them from the official website. Once you have npm, you can install `cross-env` globally using the following command:

   ```bash
   npm install -g cross-env
   ```

   Alternatively, you can install it locally in your project:

   ```bash
   npm install cross-env --save-dev
   ```

2. **Set environment variables:**

   Suppose you want to set an environment variable named `NODE_ENV` with the value `'production'`.

   In your `package.json` script section, you can use `cross-env` like this:

   ```json
   "scripts": {
     "start": "cross-env NODE_ENV=production node server.js"
   }
   ```

   In this example, the `NODE_ENV` variable is set to `'production'` while starting your Node.js server using the `node server.js` command.

3. **Using the environment variable:**

   Inside your Node.js application, you can access the `NODE_ENV` environment variable like this:

   ```javascript
   const environment = process.env.NODE_ENV;

   console.log(`Current environment: ${environment}`);
   ```

   This will output:

   ```
   Current environment: production
   ```

4. **Running the script:**

   To run the script defined in the `package.json` using `cross-env`, you can use the `npm run` command:

   ```bash
   npm run start
   ```

   `cross-env` ensures that the environment variable is set correctly regardless of the operating system, making it a useful tool for maintaining consistency across different platforms.

Remember that the key benefit of using `cross-env` is that it abstracts the differences between Windows and Unix-like systems (Linux, macOS) when setting environment variables. This helps ensure your scripts work reliably across all platforms.

### How to use SuperTest for Express Testing.

`SuperTest` is a popular testing library for Node.js that makes it easy to perform HTTP assertions and testing for Express.js applications. It allows you to make HTTP requests to your Express application and then assert the responses. Here's how you can use `SuperTest` for testing an Express application:

1. **Install SuperTest:**

   Before you begin, make sure you have Node.js and npm installed. Then, navigate to your project directory and install the necessary packages:

   ```bash
   npm install supertest express --save-dev
   ```

2. **Create an Express Application:**

   Create an Express application that you want to test. For example, let's create a simple Express app in a file named `app.js`:

   ```javascript
   const express = require('express');
   const app = express();

   app.get('/', (req, res) => {
     res.status(200).json({ message: 'Hello, World!' });
   });

   module.exports = app;
   ```

3. **Write Test Cases using SuperTest:**

   Create a test file, such as `test.js`, to write your SuperTest test cases. Here's an example of a test suite using `Mocha` and `Chai` along with `SuperTest`:

   ```javascript
   const request = require('supertest');
   const app = require('./app'); // Path to your Express app file
   const expect = require('chai').expect;

   describe('Testing Express App', () => {
     it('should return a JSON message', async () => {
       const response = await request(app).get('/');

       expect(response.status).to.equal(200);
       expect(response.body.message).to.equal('Hello, World!');
     });
   });
   ```

4. **Run Tests:**

   Use your preferred test runner to execute the test file. In this example, we'll assume you're using `Mocha`. If you haven't already, you need to install `mocha` and `chai`:

   ```bash
   npm install mocha chai --save-dev
   ```

   Then, run the tests using `mocha`:

   ```bash
   npx mocha test.js
   ```

   This will execute the test suite and display the results.

By using `SuperTest`, you're able to simulate HTTP requests to your Express application, send them, and then make assertions about the responses. This allows you to thoroughly test your Express routes, middleware, and other aspects of your application's HTTP interactions.

### Make the tests in Jest

Certainly! If you'd like to use Jest for testing your Express application with SuperTest, here's how you can do it:

1. **Install Dependencies:**

   First, make sure you have Node.js and npm installed. Then, navigate to your project directory and install the necessary packages:

   ```bash
   npm install jest supertest express --save-dev
   ```

2. **Create an Express Application:**

   Create an Express application just like in the previous example. Save it in a file named `app.js`.

3. **Write Test Cases using Jest and SuperTest:**

   Create a test file, such as `app.test.js`, to write your Jest test cases using SuperTest. Here's an example:

   ```javascript
   const request = require('supertest');
   const app = require('./app'); // Path to your Express app file

   describe('Testing Express App', () => {
     it('should return a JSON message', async () => {
       const response = await request(app).get('/');

       expect(response.status).toBe(200);
       expect(response.body.message).toBe('Hello, World!');
     });
   });
   ```

4. **Configure Jest:**

   Jest expects test files to follow the naming pattern `<filename>.test.js`. Make sure your test file is named accordingly (`app.test.js` in this case). Jest will automatically find and run the test files with this naming convention.

5. **Run Tests:**

   To run the tests, simply use the `jest` command:

   ```bash
   npx jest
   ```

   Jest will execute the test suite and display the results.

By using Jest with SuperTest, you can write expressive test cases for your Express application, and Jest's built-in assertion library makes it easy to write clean and readable assertions. SuperTest continues to help you simulate HTTP requests and test your application's behavior under various scenarios.

### How to jump tests that do not interest that they run.

In Jest, you can use the `.skip` function to temporarily exclude specific tests or test suites from running. This can be useful when you want to ignore certain tests that you're not currently interested in running. Here's how you can do it:

1. **Skipping Individual Tests:**

   To skip a specific test, you can use the `.skip` function within a test block. Here's an example:

   ```javascript
   describe('My test suite', () => {
     it.skip('should run this test', () => {
       // Test code here
     });

     it('should skip this test', () => {
       // This test will be skipped
     });
   });
   ```

   In the above example, the first test will be executed, while the second test will be skipped.

2. **Skipping Test Suites:**

   If you want to skip an entire test suite, you can use the `.skip` function with `describe`. Here's an example:

   ```javascript
   describe.skip('My skipped test suite', () => {
     it('should skip all tests in this suite', () => {
       // This test will be skipped
     });
   });

   describe('My regular test suite', () => {
     it('should run this test', () => {
       // Test code here
     });
   });
   ```

   In this example, all tests within the "My skipped test suite" will be skipped.

3. **Running Skipped Tests:**

   To run skipped tests, you can use the `--runInBand` flag with `jest` followed by the specific test or test suite name. For example:

   ```bash
   npx jest --runInBand MyTestSuiteName
   ```

   Replace `MyTestSuiteName` with the name of the test suite containing the skipped test(s). This will run only the specified test suite, including the skipped tests within it.

Remember that skipping tests too often can lead to stale code and untested functionality. It's generally better to have a good test suite that runs all relevant tests, but skipping can be useful in situations where tests are temporarily irrelevant or need to be excluded for debugging purposes.

### Avoid depending on Side Effects in your tests.

Depending on side effects in tests can lead to fragile and unreliable tests. Tests that rely heavily on external dependencies or produce side effects can be difficult to maintain and can result in false positives or negatives. Here are some strategies to avoid depending on side effects in your tests:

1. **Isolate Dependencies:**

   Use techniques like mocking and stubbing to isolate external dependencies. Mocking libraries, like `jest.mock()` in Jest, allow you to replace external dependencies with controlled implementations, ensuring that your tests only focus on the behavior of the unit being tested.

2. **Dependency Injection:**

   Instead of hardcoding dependencies within your code, inject them as parameters or properties. This allows you to provide mock or stub implementations during testing. Dependency injection promotes loose coupling and better testability.

3. **Use Fixtures and Factories:**

   Create fixture data and test factories that generate consistent and controlled input data for your tests. This ensures that your tests are not affected by changes in external data sources or APIs.

4. **Avoid Global State:**

   Global state can introduce unpredictability and side effects. When writing tests, ensure that your code doesn't rely heavily on global variables or shared state that can change between tests.

5. **Test Immutability:**

   Write tests that validate your code's ability to handle immutable data. This helps avoid unintended side effects that can occur when modifying shared data.

6. **Use Setup and Teardown:**

   Many testing frameworks provide setup (`beforeEach`, `beforeAll`) and teardown (`afterEach`, `afterAll`) hooks. Use these hooks to ensure a consistent initial state before each test and to clean up any side effects after each test.

7. **Test Pure Functions:**

   Whenever possible, write tests for pure functions that don't have side effects. Pure functions always produce the same output for the same input, making them easier to test and reason about.

8. **Isolate Side Effects:**

   If you're testing code with side effects, try to isolate those effects and test them separately from the core logic. This might involve testing database interactions, network requests, or filesystem operations in dedicated test suites.

9. **Use Property-Based Testing:**

   Property-based testing libraries, like `fast-check` or `jsverify`, generate a wide range of test cases based on properties you define. This can help uncover unexpected side effects or corner cases in your code.

By avoiding heavy reliance on side effects and focusing on isolated and controlled tests, you can create more robust and maintainable test suites that accurately reflect the behavior of your code. This also helps ensure that your tests continue to work even as external dependencies change or evolve.

