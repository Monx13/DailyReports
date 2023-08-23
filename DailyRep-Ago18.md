# *Daily Report Ago/18/2023*
 
- [*Daily Report Ago/18/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
    - [*MongoDB*](#mongodb)
    - [*MongoDB Atlas*](mongodb-atlas)
    - [*Create MongoDB Collection*](#create-mongodb-collection)
    - [*To query MongoDB*](#to-query-mongodb)
    - [*How to make a connection from our database to a client*](#how-to-make-a-connection-from-our-database-to-a-client)
    - [*Insert documents into mongodb*](#insert-documents-into-mongodb)
    - [*Find a document with filter in mongodb*](#find-a-document-with-filter-in-mongodb)
---

## **STATUS**
- I'm in video 8 🍃 Learn MongoDB from scratch! + Deploy Database with Atlas 📡 (Bootcamp FullStack JavaScript).

- To learn the backend, we're going to need a place to persist our data. For this we are going to use one of the most famous databases of the moment: MongoDB.

- Also, with MongoDB Atlas, we are going to deploy a database completely free of charge.

- A new Part 3 folder is created in the repository. [Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)


[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)

[Fullstack Bootcamp Course](https://fullstackopen.com/es/)

## **BLOCKERS**
- None

## **NOTES**

### MongoDB
To store our saved notes indefinitely, we need a database. Most of the courses taught at the University of Helsinki use relational databases. In this course we will use MongoDB, which is the so-called document database.

Document databases differ from relational databases in how they organize data, as well as the query languages they support. Document databases are generally classified under the umbrella term NoSQL.

Naturally, you can install and run MongoDB on your own computer. However, the Internet is also full of Mongo database services that you can use. Our preferred MongoDB provider in this course will be MongoDB Atlas.

NoSQL (Not Only SQL) databases are a category of database management systems that depart from the traditional relational database model. Unlike SQL databases, which use rigid tables and schemas, NoSQL databases allow flexibility in how data is stored and retrieved.

NoSQL databases are especially suitable for applications that handle large volumes of unstructured or semi-structured data, such as social networks, sensors, web application logs, and much more. These databases can use various data models, such as documents, columns, graphs, or key-value pairs, to accommodate different types of information and storage needs.

Each NoSQL database model has its own characteristics and advantages, allowing developers to choose the best option for their specific application.

### MongoDB Atlas
MongoDB Atlas is a cloud service that provides a fully managed and scalable database platform for MongoDB. It is developed by the same company behind MongoDB and is designed to simplify the deployment, management, and scaling of MongoDB databases in the cloud.

Some of the features of MongoDB Atlas include:

1. **Automated Administration:** Atlas takes care of tasks such as database configuration, provisioning, backups and monitoring, reducing the operational burden on development teams.

2. **Scalability:** You can increase or decrease the size of your database clusters according to your needs, allowing you to scale horizontally efficiently.

3. **Security:** Atlas offers security options such as authentication, data encryption at rest and in transit, as well as the ability to implement network firewalls.

4. **Backup and Restore:** Atlas performs scheduled automatic backups and allows you to restore data in case of problems.

5. **Monitoring:** Provides detailed information about the performance of the database and the infrastructure, which helps to optimize the performance of the applications.

6. **Multi-Cloud Deployment:** Atlas offers the ability to deploy MongoDB databases on multiple cloud providers, such as AWS, Google Cloud, and Azure.

In short, MongoDB Atlas is a convenient solution for deploying and managing MongoDB databases in the cloud without the need to worry about the underlying infrastructure and manual administration.

### Create MongoDB Collection

To create a collection in MongoDB, you can follow these steps using the MongoDB client or the command line interface (mongo shell):

1. **Start the MongoDB Client or mongo shell:** Open the MongoDB client in your terminal. You can run `mongo` to open the MongoDB shell.

2. **Select Database:** If you haven't already selected the database in which you want to create the collection, use the `use_database_name` command.

3. **Create Collection:** Use the `createCollection()` method to create the collection. For example, if you want to create a collection called "users", you can use the following command:
   
    ```javascript
    db.createCollection("users");
    ```

    If you want to specify additional options when creating the collection, you can do so by passing an object with the options as an argument. For example:

    ```javascript
    db.createCollection("users", { capped: true, size: 5242880, max: 5000 });
    ```

    In this example, a collection called "users" is created with a size limitation and a maximum document limit.

4. **Verify Creation:** You can verify that the collection was created correctly by using the `show collections` command to list all the collections in the current database.

Remember that in MongoDB, collections are automatically created when the first document is inserted into them. You don't need to explicitly create a collection if you plan to insert data into it after creation.

### To query MongoDB
To query MongoDB, you can use the mongo shell or a MongoDB library in your preferred programming language. Here is a basic example of how to make a query using the mongo shell:

1. **Start the mongo shell:** Open your terminal and run the `mongo` command to start the MongoDB shell.

2. **Select Database:** Use the `use_database_name` command to select the database you want to query.

3. **Run Query:** Use the `find()` method to query a specific collection. For example, if you want to get all the documents in the "users" collection, you can do it like this:

    ```javascript
    db.users.find();
    ```

    This will return all the documents in the "users" collection. You can add query criteria to filter the results. For example, to find all users with the name "John", you could use:

    ```javascript
    db.users.find({ name: "John" });
    ```

    Also, you can match only certain fields by using the second argument to the `find()` method. For example:

    ```javascript
    db.users.find({ name: "John" }, { _id: 0, name: 1, age: 1 });
    ```

    In this example, only the "name" and "age" fields are projected, and the "_id" field is excluded.

### How to make a connection from our database to a client

To establish a connection between your MongoDB database and a client (such as a web app or mobile app), you need to use the appropriate driver or library in the programming language you're using. Here is an overview of the steps you need to follow:

1. **Select a Driver:** MongoDB offers official and community drivers for several programming languages, including Python, Node.js, Java, C#, and more. You must choose the driver that is compatible with the programming language in which you are developing your application.

2. **Install Driver:** Install the corresponding MongoDB driver using a package management tool for your programming language. For example, if you're using Node.js, you can use npm or yarn to install the driver package.

3. **Import Controller:** Import or include the controller in your application using the appropriate syntax for your programming language. This usually involves a `require` or `import` statement.

4. **Establish Connection:** Use the function or method provided by the driver to establish a connection to your MongoDB database. To do this, you need to provide the MongoDB connection URL, which is typically in the following format:

    ```
    mongodb://user:password@host:port/database_name
    ```

5. **Perform Operations:** Once the connection is established, you can use the methods provided by the driver to perform operations on the database, such as insert, query, update, and delete data.

Here's a basic JavaScript example using the official MongoDB driver for Node.js:

```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://user:password@localhost:27017/database_name';

MongoClient.connect(url, (err, client) => {
   if (err) {
     console.error('Error connecting to database:', err);
     return;
   }
  
   console.log('Connection successful');
  
   // Perform database operations here
  
   client.close();
});
```

Remember to replace `username`, `password`, `localhost`, `27017`, and `database_name` with the correct values based on your configuration.

### Insert documents into mongodb

To insert documents into MongoDB, you can use the `insertOne()` or `insertMany()` method depending on whether you want to insert a single document or multiple documents at once. Here are examples of how to do it using the mongo shell:

1. **Insert a Single Document:**
   
    Use the `insertOne()` method to insert a single document into a collection. For example, to insert a document into the "users" collection, you could do the following:

    ```javascript
    db.users.insertOne({
      name: "John",
      age: 30,
      email: "john@example.com"
    });
    ```

2. **Insert Multiple Documents:**

    Use the `insertMany()` method to insert multiple documents into a collection. For example, to insert three documents into the "products" collection, you could do the following:

    ```javascript
    db.products.insertMany([
      { name: "T-shirt", price: 20 },
      { name: "Pants", price: 40 },
      { name: "Shoes", price: 60 }
    ]);
    ```

Remember that if you have not explicitly created the collection before inserting the documents, MongoDB will create it automatically when you insert the first document.

Note that in most cases MongoDB libraries and drivers in programming languages will provide similar methods for performing document inserts into the database. It is important to follow data security and validation best practices when inserting documents into your database.

### Find a document with filter in mongodb

Para buscar un documento con un filtro en MongoDB, puedes utilizar el método `find()` junto con un objeto que contiene los criterios de búsqueda. Aquí tienes un ejemplo de cómo hacerlo utilizando la mongo shell:

Supongamos que tienes una colección llamada "usuarios" y deseas buscar usuarios cuya edad sea mayor o igual a 25:

```javascript
db.usuarios.find({ edad: { $gte: 25 } });
```

En este ejemplo, el `{ edad: { $gte: 25 } }` es el filtro que especifica la condición de búsqueda. `$gte` es un operador de comparación que significa "mayor o igual". Esto devolverá todos los documentos de la colección "usuarios" que cumplan con el criterio de edad.

También puedes combinar múltiples criterios en un filtro. Por ejemplo, si deseas buscar usuarios con una edad mayor o igual a 25 y que vivan en una ciudad específica:

```javascript
db.usuarios.find({ edad: { $gte: 25 }, ciudad: "Ciudad Ejemplo" });
```

Recuerda que MongoDB ofrece varios operadores de comparación y lógicos que puedes utilizar para construir filtros más complejos. Si estás utilizando un lenguaje de programación con un controlador de MongoDB, los métodos para realizar búsquedas serán similares, pero con la sintaxis correspondiente al lenguaje en cuestión.
