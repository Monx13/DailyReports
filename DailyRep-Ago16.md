# *Daily Report Ago/16/2023*

---
 
- [*Daily Report Ago/16/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
    - [\* *Nodemon* \*](#nodemon)
    - [\* *Installation nodemon* \*](#installation_nodemon)
    - [\* *Usage* \*](#usage)
---


## **STATUS**

- Video 6 is part 3 of the Fullstack course. In this part, our focus shifts to the backend, that is, to the implementation of the functionality on the server side. We will implement a simple REST API in Node.js using the Express library, and the application data will be stored in a MongoDB database. At the end of this part, we will deploy our application to the Internet.

- In video 6 we are shown how to use Node.js to create a server. "Learning Node.JS and Express to create an API".

- We learn how to install node.js as well as how to use it in a simple way with a "Hello world" from node.js.

- We create a server with node.js for the API.

- We use Nodemon and learn how to install it and some uses.

- A new Part 3 folder is created in the repository. [Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)


[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)
[Fullstack Bootcamp Course](https://fullstackopen.com/es/)

---
## **BLOCKERS**

- None.
---

## **NOTES**

### * *Nodemon* *

nodemon is a tool that helps develop Node.js based applications by automatically restarting the node application when file changes in the directory are detected.

nodemon does not require any additional changes to your code or method of development. nodemon is a replacement wrapper for node. To use nodemon, replace the word node on the command line when executing your script.

### * *Installation nodemon* *
Either through cloning with git or by using npm (the recommended way):
```
npm install -g nodemon # or using yarn: yarn global add nodemon
```

And nodemon will be installed globally to your system path.

You can also install nodemon as a development dependency:
```
npm install --save-dev nodemon # or using yarn: yarn add nodemon -D
```
With a local installation, nodemon will not be available in your system path or you can't use it directly from the command line. Instead, the local installation of nodemon can be run by calling it from within an npm script (such as npm start) or using npx nodemon.

### * *Usage* *
nodemon wraps your application, so you can pass all the arguments you would normally pass to your app:
```
nodemon [your node app]
```
For CLI options, use the -h (or --help) argument:
```
nodemon -h
```
Using nodemon is simple, if my application accepted a host and port as the arguments, I would start it as so:

```
nodemon ./server.js localhost 8080
```
Any output from this script is prefixed with [nodemon], otherwise all output from your application, errors included, will be echoed out as expected.

You can also pass the inspect flag to node through the command line as you would normally:
```
nodemon --inspect ./server.js 80
```
If you have a package.json file for your app, you can omit the main script entirely and nodemon will read the package.json for the main property and use that value as the app (ref).

nodemon will also search for the scripts.start property in package.json (as of nodemon 1.1.x).

Also check out the FAQ or issues for nodemon.
