# *Daily Report Ago/17/2023*
 
- [*Daily Report Ago/17/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
    - [*middlewares*](#middlewares)
    - [*CORS issues*](#cors_issues)
    - [*Heroku CLI*](#heroku_cli)
---

## **STATUS**

- Video 7 is the continuation of video 6, the API that was created with Node.js continues to be built and new extensions are added according to the required tools.

- ESLint is added and configured.

- It is known that they are Middlewares in Express and how we should use them for the API.

- CORS problems arise and midudev explains how we should solve them or what we can consult to fix them.

- Heroku CLI is used, the application is installed and created.

- A new Part 3 folder is created in the repository. [Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)


[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)

[Fullstack Bootcamp Course](https://fullstackopen.com/es/)


## **BLOCKERS**

- None.
---

## **NOTES**

### ***middlewares***

In the context of Express.js, middlewares are functions that are executed in the processing flow of an HTTP request before a response is sent. Middlewares in Express have access to the request and response objects, and can perform various tasks, such as modifying request or response data, authenticating users, performing validation, logging information, and so on. Middlewares are a fundamental part of the Express architecture and allow you to build web applications in a modular and scalable way.

Here is a basic description of how the middlewares work in Express:

Definition of Middlewares: Middlewares are functions that are defined by app.use() or app.METHOD() (where METHOD is an HTTP method like get, post, put, delete, etc.). You can add middlewares at the application level (applies to all routes) or at the route level (applies only to specific routes).

Order of Execution: Middlewares are executed in the order in which they are defined in your code. Each middleware can decide whether to pass the request to the next middleware or send a response. If a middleware decides to send a response, the execution flow stops and the remaining middlewares will not be executed.

Data Passing: Middlewares can modify the request and response objects. They can add properties, change values, perform validations, etc. In addition, they can pass data from one middleware to another using the properties of the request object.

Example of using middlewares in Express:

```js
const express = require('express');
const app = express();

// Middleware de nivel de aplicación
app.use((req, res, next) => {
    console.log('Middleware de nivel de aplicación');
    next(); // Llama al siguiente middleware
});

// Middleware de nivel de ruta
app.get('/', (req, res, next) => {
    console.log('Middleware de nivel de ruta');
    next(); // Llama al siguiente middleware
}, (req, res) => {
    res.send('Hola, mundo!');
});

app.listen(3000, () => {
    console.log('Servidor Express iniciado en el puerto 3000');
});

```
In this example, there are two middlewares. The first is an application-level middleware that runs for all routes. The second is a path-level middleware that is executed only when the parent path ("/") is accessed. Each middleware calls next() to pass the request to the next middleware.

Middlewares are a powerful feature of Express that allow you to effectively modularize and organize your code by handling different aspects of requests and responses in your web application.

### ***CORS issues***

CORS (Cross-Origin Resource Sharing) issues are common in web development when trying to make requests (such as AJAX requests) from one origin (domain, port, or protocol) to another. CORS is a security measure implemented by browsers to prevent a malicious website from accessing resources on another site without permission. When CORS issues, it's usually due to browser-imposed restrictions that block cross-origin requests.

Some of the most common issues and challenges related to CORS are:

1. **Requests from a different origin:** Browsers by default block AJAX (or Fetch API) requests to a server with a different origin than the requesting site. This can cause errors like "Blocked by CORS policy" in the browser console.

2. **Header exchange not allowed:** CORS requests include HTTP headers that provide additional information about the request or response. Some headers require explicit permissions on the server to be exchanged.

3. **Request methods not allowed:** Some HTTP methods (such as DELETE, PUT, etc.) may require additional configuration on the server to allow requests from other sources.

4. **Cookies and authentication:** Cookies and authentication headers (such as credentials) may require special configuration to work properly on CORS requests.

5. **Preflight requests:** Some CORS requests trigger additional "preflight" requests, which are OPTIONS requests sent before the actual request. These requests must be handled correctly on the server.

To troubleshoot CORS, you can do the following:

1. **Configure the server:** Make sure the server allows CORS requests from the necessary origins. This usually involves setting the appropriate CORS headers in the server's responses.

2. **Use proxies:** You can set up a proxy on your server to redirect requests to other domains and avoid CORS issues on the client side.

3. **Allow specific methods and headers:** Make sure the server allows the HTTP methods and headers needed in CORS requests.

4. **Enable credentials:** If you need to send cookies or credentials in CORS requests, configure the server to allow credentials.

5. **Configure response headers:** Make sure the response headers include the necessary CORS headers.

6. **Using middleware or libraries:** In frameworks like Express.js, you can use middleware like "cors" to simplify CORS configuration.

Remember that the specific configuration for troubleshooting CORS may vary depending on the server, programming language, and libraries you are using.

### ***Heroku CLI***

The Heroku Command Line Interface (CLI) is a command line tool that allows you to interact with the Heroku platform from your computer's terminal. With the Heroku CLI, you can manage and deploy applications on the Heroku cloud, as well as perform a variety of application development and management tasks.

Some of the functionality you can perform with the Heroku CLI include:

1. **Application Deployment:** You can create, deploy and manage your applications on the Heroku platform. This includes uploading your code, defining environment variables, scaling instances, and more.

2. **Addon Management:** You can add and manage addons such as databases, caching systems and monitoring tools for your applications.

3. **Resource Scaling:** You can scale your applications to handle different traffic loads, either vertically (more resources on one instance) or horizontally (more instances).

4. **Environment Variable Management:** You can set and modify environment variables that are used by your application, such as secret keys and specific settings.

5. **Viewing Logs:** You can access and view your application's logs to monitor its behavior and detect problems.

6. **Remote Command Execution:** You can execute commands directly on your cloud application using the CLI.

To get started with the Heroku CLI, follow these steps:

1. **Installation:** Download and install the Heroku CLI from the official Heroku website or use a package manager (such as Homebrew on macOS).

2. **Authentication:** Open the terminal and run `heroku login`. You will be prompted to sign in with your Heroku account in your browser.

3. **Usage:** Once authenticated, you can use CLI commands to manage your applications, deploy code, set environment variables, and more.

Here are some sample Heroku CLI commands:

- `heroku create`: Create a new app on Heroku.
- `heroku logs`: Shows the application logs.
- `heroku addons:add`: Add an addon to your application.
- `heroku config:set`: Set environment variables.

Remember to consult the official Heroku documentation and CLI help (`heroku help`) for more details on how to use the tool and perform specific tasks.