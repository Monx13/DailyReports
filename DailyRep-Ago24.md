# *Daily Report Aug/24/2023*
 
- [*Daily Report Aug/24/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
---

## **STATUS**
- Video 12 CREATE Users and ADD SECURITY to your PASSWORDS 🔒 in MongoDB (FullStack JavaScript Bootcamp).
- We create a relationship between our backend and the users. We will review some good practices when saving passwords in the database and add tests.
- We learn:
  - How to relate collections in NoSQL?
  - Creating the User Model in Mongoose
  - Creating Controller for User endpoints
  - Testing our endpoints to create users

[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)

[Fullstack Bootcamp Course](https://fullstackopen.com/es/)

## **BLOCKERS**
- I can't upload remote repositories due to changing the hard drive of the pc. I am configuring or adding a new HSS key but it gives me an error.

## **NOTES**

### How to relate collections in NoSQL?

In NoSQL databases, data is typically stored in a way that allows for flexible and efficient handling of complex relationships without relying on traditional relational database structures. Different NoSQL databases have various methods for relating collections or documents. Here, I'll provide you with general concepts and examples based on common types of NoSQL databases:

1. **Document-Oriented Databases (e.g., MongoDB):**
   In document-oriented databases, collections are akin to tables in relational databases, and documents are similar to rows. Relationships can be handled in a few ways:

   - **Embedding Documents:** You can nest documents within documents. For example, if you have a "users" collection and a "comments" collection, you might embed the comments within the user document. This is suitable when the related data is relatively small and doesn't change often.
   
     ```json
     {
       "_id": ObjectId("user_id"),
       "name": "John Doe",
       "comments": [
         {"text": "Great article!", "date": "2023-08-29"},
         {"text": "I enjoyed reading this.", "date": "2023-08-30"}
       ]
     }
     ```

   - **Referencing Documents:** You can store references to related documents. For example, you could store the ID of a user in the comment document. This is suitable when related data can change frequently and needs to be updated independently.
   
     User document:
     ```json
     {
       "_id": ObjectId("user_id"),
       "name": "John Doe"
     }
     ```

     Comment document:
     ```json
     {
       "_id": ObjectId("comment_id"),
       "user_id": ObjectId("user_id"),
       "text": "Great article!",
       "date": "2023-08-29"
     }
     ```

2. **Graph Databases (e.g., Neo4j):**
   Graph databases are designed to handle relationships explicitly. Nodes represent entities, and relationships between nodes are first-class citizens. In a graph database, relationships are integral to the data structure.

   For example, if you have "users" and "posts," you would create nodes for users and posts, and then create relationships between them to represent comments or likes.

3. **Key-Value Stores (e.g., Redis):**
   Key-value stores are simple and efficient databases that store data as key-value pairs. While they don't inherently support complex relationships like document or graph databases, you can still model relationships by using compound keys or storing serialized data within values.

   For instance, if you're storing user profiles and their posts in Redis, you could use keys like "user:user_id" and "post:post_id" to store related data and then use programmatic logic to manage relationships.

Remember that the choice of how to model relationships in a NoSQL database depends on your specific use case, access patterns, and the trade-offs you're willing to make in terms of query performance, data duplication, and consistency. Always consider the strengths and limitations of the NoSQL database you're using and design your data model accordingly.

### Creating the User Model in Mongoose

Creating a user model in Mongoose, which is an Object Data Modeling (ODM) library for MongoDB in Node.js, involves defining a schema for your user data and then creating a model based on that schema. Here's a step-by-step guide to creating a basic user model using Mongoose:

1. **Install Mongoose:**
   If you haven't already, install Mongoose using npm or yarn:

   ```bash
   npm install mongoose
   # or
   yarn add mongoose
   ```

2. **Create the User Schema:**
   In your Node.js application, create a file (e.g., `userModel.js`) where you'll define the schema for your user data. Import Mongoose and define the schema using the `mongoose.Schema` class.

   ```javascript
   const mongoose = require('mongoose');

   const userSchema = new mongoose.Schema({
     username: { type: String, required: true },
     email: { type: String, required: true, unique: true },
     password: { type: String, required: true },
     createdAt: { type: Date, default: Date.now }
   });

   module.exports = mongoose.model('User', userSchema);
   ```

   In this example, the user schema has fields for `username`, `email`, `password`, and `createdAt`.

3. **Connect to MongoDB:**
   Before using the model, you need to establish a connection to your MongoDB database. This is typically done in your application's entry point (e.g., `app.js` or `index.js`).

   ```javascript
   const mongoose = require('mongoose');
   
   mongoose.connect('mongodb://localhost/myapp', {
     useNewUrlParser: true,
     useUnifiedTopology: true
   })
   .then(() => {
     console.log('Connected to MongoDB');
   })
   .catch(err => {
     console.error('Error connecting to MongoDB:', err);
   });
   ```

   Replace `'mongodb://localhost/myapp'` with your actual MongoDB connection string.

4. **Using the User Model:**
   Now that you've defined the user model, you can use it to interact with your MongoDB database. Here's an example of creating a new user and saving it to the database:

   ```javascript
   const User = require('./userModel'); // Import the User model
   
   // Create a new user instance
   const newUser = new User({
     username: 'john_doe',
     email: 'john@example.com',
     password: 'secretpassword'
   });
   
   // Save the user to the database
   newUser.save()
     .then(savedUser => {
       console.log('User saved:', savedUser);
     })
     .catch(err => {
       console.error('Error saving user:', err);
     });
   ```

Remember to handle errors and asynchronous operations appropriately in your code. The example above provides a basic foundation for creating and using a user model in Mongoose. You can expand on this by adding validation, encryption for passwords, additional methods, and more according to your application's requirements.

### Creating Controller for User endpoints

Creating controllers for user endpoints involves defining functions that handle HTTP requests and interact with your Mongoose models to perform CRUD (Create, Read, Update, Delete) operations on user data. Here's a step-by-step guide to creating a basic user controller for handling user-related endpoints:

1. **Create a Controller File:**
   In your project directory, create a new file for your user controller (e.g., `userController.js`).

2. **Import Dependencies:**
   In your controller file, import the necessary dependencies, including the Mongoose user model and any other modules you might need.

   ```javascript
   const User = require('./userModel'); // Import the User model
   // Other dependencies if needed
   ```

3. **Define Controller Functions:**
   Define functions for different CRUD operations. Below are examples for common operations:

   ```javascript
   const userController = {
     // Create a new user
     createUser: async (req, res) => {
       try {
         const { username, email, password } = req.body;
         const newUser = new User({ username, email, password });
         const savedUser = await newUser.save();
         res.status(201).json(savedUser);
       } catch (error) {
         res.status(400).json({ error: error.message });
       }
     },

     // Get all users
     getAllUsers: async (req, res) => {
       try {
         const users = await User.find();
         res.status(200).json(users);
       } catch (error) {
         res.status(500).json({ error: error.message });
       }
     },

     // Get a user by ID
     getUserById: async (req, res) => {
       try {
         const user = await User.findById(req.params.id);
         if (!user) {
           return res.status(404).json({ error: 'User not found' });
         }
         res.status(200).json(user);
       } catch (error) {
         res.status(500).json({ error: error.message });
       }
     },

     // Update a user by ID
     updateUserById: async (req, res) => {
       try {
         const updatedUser = await User.findByIdAndUpdate(
           req.params.id,
           req.body,
           { new: true }
         );
         if (!updatedUser) {
           return res.status(404).json({ error: 'User not found' });
         }
         res.status(200).json(updatedUser);
       } catch (error) {
         res.status(400).json({ error: error.message });
       }
     },

     // Delete a user by ID
     deleteUserById: async (req, res) => {
       try {
         const deletedUser = await User.findByIdAndDelete(req.params.id);
         if (!deletedUser) {
           return res.status(404).json({ error: 'User not found' });
         }
         res.status(204).end();
       } catch (error) {
         res.status(500).json({ error: error.message });
       }
     }
   };

   module.exports = userController;
   ```

4. **Set Up Routes:**
   In your main application file (e.g., `app.js`), set up routes that use the controller functions you've defined.

   ```javascript
   const express = require('express');
   const app = express();
   const userController = require('./userController'); // Import the user controller

   // Middleware and other configurations if needed

   // Define routes
   app.post('/users', userController.createUser);
   app.get('/users', userController.getAllUsers);
   app.get('/users/:id', userController.getUserById);
   app.put('/users/:id', userController.updateUserById);
   app.delete('/users/:id', userController.deleteUserById);

   // Start the server
   const PORT = process.env.PORT || 3000;
   app.listen(PORT, () => {
     console.log(`Server is running on port ${PORT}`);
   });
   ```

This is a basic example of how you can create a user controller to handle CRUD operations for user endpoints. Depending on your application's complexity, you might need to add input validation, authentication, error handling, and other features to enhance the functionality and security of your endpoints.

### Testing our endpoints to create users

Testing your endpoints is an essential part of the development process to ensure that your code works as expected and handles different scenarios correctly. For testing your user creation endpoint, you can use testing frameworks like Mocha, Chai, and Supertest. Here's a guide on how to set up and test your user creation endpoint using these tools:

1. **Install Dependencies:**
   Make sure you have Mocha, Chai, and Supertest installed in your project. You can install them using npm or yarn:

   ```bash
   npm install mocha chai supertest --save-dev
   # or
   yarn add mocha chai supertest --dev
   ```

2. **Create a Test File:**
   Create a test file (e.g., `userController.test.js`) in a directory named `test`.

3. **Write Tests:**
   In your test file, import the necessary dependencies and the user controller. Then, write tests to cover different scenarios for creating users.

   ```javascript
   const chai = require('chai');
   const expect = chai.expect;
   const request = require('supertest');
   const app = require('../app'); // Your Express app
   const User = require('../userModel'); // Your User model

   describe('User Controller', () => {
     beforeEach(async () => {
       // Clear the users collection before each test
       await User.deleteMany({});
     });

     describe('POST /users', () => {
       it('should create a new user', async () => {
         const user = {
           username: 'john_doe',
           email: 'john@example.com',
           password: 'secretpassword'
         };

         const response = await request(app)
           .post('/users')
           .send(user);

         expect(response.status).to.equal(201);
         expect(response.body.username).to.equal(user.username);
         expect(response.body.email).to.equal(user.email);

         // Check if the user is actually saved in the database
         const savedUser = await User.findById(response.body._id);
         expect(savedUser).to.exist;
         expect(savedUser.username).to.equal(user.username);
         expect(savedUser.email).to.equal(user.email);
       });

       it('should handle invalid user data', async () => {
         const invalidUser = {
           // Missing required fields
         };

         const response = await request(app)
           .post('/users')
           .send(invalidUser);

         expect(response.status).to.equal(400);
         // Add more assertions as needed
       });
     });

     // Add more test cases for other scenarios
   });
   ```

4. **Run Tests:**
   In your terminal, run your tests using the testing framework's command. For Mocha, you can use the following command:

   ```bash
   npx mocha test/userController.test.js
   ```

   This command will execute the tests you've written and provide output indicating whether the tests passed or failed.

Remember to customize the test cases to match your application's functionality and expected behaviors. Additionally, you might need to adjust the import paths and other configurations based on your project structure.