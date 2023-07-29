# *Daily Report Jul/28/2023*

---
 
- [*Daily Report Jul/28/2023*](#daily-report-jul282023)
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
    - [Introduction to React](#introduction-to-react)
    - [Component](#component)
    - [JS](#js)
    - [props](#props)
---

## **STATUS**

- I was able to fix the files error by creating a new folder with react's create. for some reason the .git was not generated like the previous time, so it was easier to upload the changes to the repository as a file folder and not as a submodule.

- I made the changes according to the progress I already had, and uploaded the new commit to the repository.
[Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)

- I looked for the page where midudev is based for the course.
[Fullstack Bootcamp](https://fullstackopen.com/es/)

- I started watching video 3 "React ⚛️: Component State, Conditional Rendering, and Events" for the FullStack Bootcamp course. 
[Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)
---

## **BLOCKERS**

- None
---

## **NOTES**

### * *Introduction to React* *

Let's create an application called part1 and navigate to its directory.

```cmd
npx create-react-app part1
cd part1
```

The application runs as follows
```cmd
npm start
```

### * *Component* *

The file App.js now defines a React component with the name App. The command on the final line of file index.js renders its contents into the div-element, defined in the file public/index.html, having the id value 'root'.

```js
ReactDOM.createRoot(document.getElementById('root')).render(<App />)
```

There are a few ways to define functions in JavaScript. Because the function consists of only a single expression we have used a shorthand, which represents this piece of code:

``` js
const App = () => {
  return (
    <div>
      <p>Hello world</p>
    </div>
  )
}
```
### * *JS* *

In practice, JSX is much like HTML with the distinction that with JSX you can easily embed dynamic content by writing appropriate JavaScript within curly braces. The idea of JSX is quite similar to many templating languages, such as Thymeleaf used along with Java Spring, which are used on servers.

JSX is "XML-like", which means that every tag needs to be closed. For example, a newline is an empty element, which in HTML can be written as follows:

```js
<br>copy
```
but when writing JSX, the tag needs to be closed:

```js
<br />
```

### * *props* *

It is possible to pass data to components using so-called props.

Let's modify the component Hello as follows:

```js
const Hello = (props) => {
  return (
    <div>
      <p>Hello {props.name}</p>
    </div>
  )
}copy
```

Now the function defining the component has a parameter props. As an argument, the parameter receives an object, which has fields corresponding to all the "props" the user of the component defines.

The props are defined as follows:

```js
const App = () => {
  return (
    <div>
      <h1>Greetings</h1>
      <Hello name='George' />
      <Hello name='Daisy' />
    </div>
  )
}copy
```

There can be an arbitrary number of props and their values can be "hard-coded" strings or the results of JavaScript expressions. If the value of the prop is achieved using JavaScript it must be wrapped with curly braces.

Let's modify the code so that the component Hello uses two props:

```js
const Hello = (props) => {
  console.log(props)
  return (
    <div>
      <p>
        Hello {props.name}, you are {props.age} years old
      </p>
    </div>
  )
}

const App = () => {
  const name = 'Peter'
  const age = 10

  return (
    <div>
      <h1>Greetings</h1>
      <Hello name='Maya' age={26 + 10} />
      <Hello name={name} age={age} />
    </div>
  )
}copy
```

The props sent by the component App are the values of the variables, the result of the evaluation of the sum expression and a regular string.