# *Daily Report Ago/15/2023*

---
 
- [*Daily Report Ago/15/2023*]
  - [**STATUS**](#status)
  - [**BLOCKERS**](#blockers)
  - [**NOTES**](#notes)
    - [\* *Inline styles* \*](#Inline_styles)
---


## **STATUS**

- With video 5 part 2 of the fullstack course ends. Let's continue our introduction to React. First, we will take a look at how to render a data collection, like a list of names, to the screen. After this, we will inspect how a user can submit data to a React application using HTML forms. Next, our focus shifts towards looking at how JavaScript code in the browser can fetch and handle data stored in a remote backend server. Lastly, we will take a quick look at a few simple ways of adding CSS styles to our React applications.

- I finished video 5 of the course 📡 Fetching and Mutating Data in React with the useEffect hook. [Fullstack Bootcamp Youtube](https://www.youtube.com/playlist?list=PLV8x_i1fqBw0Kn_fBIZTa3wS_VZAqddX7)

- Video 6 is part 3 of the Fullstack course. In this part, our focus shifts to the backend, that is, to the implementation of the functionality on the server side. We will implement a simple REST API in Node.js using the Express library, and the application data will be stored in a MongoDB database. At the end of this part, we will deploy our application to the Internet.



- I made the changes according to the progress I already had, and uploaded the new commit to the repository.
[Fullstack Bootcamp Repository](https://github.com/Monx13/midudev-bootcamp-course)




[Fullstack Bootcamp Course](https://fullstackopen.com/es/)

---
## **BLOCKERS**

- I had to reinstall node.js on my computer.
---

## **NOTES**

### * *Inline styles* *


React also makes it possible to write styles directly in the code as so-called inline styles.

The idea behind defining inline styles is extremely simple. Any React component or element can be provided with a set of CSS properties as a JavaScript object through the style attribute.

CSS rules are defined slightly differently in JavaScript than in normal CSS files. Let's say that we wanted to give some element the color green and italic font that's 16 pixels in size. In CSS, it would look like this:

```css
{
  color: green;
  font-style: italic;
  font-size: 16px;
}copy
But as a React inline-style object it would look like this:

{
  color: 'green',
  fontStyle: 'italic',
  fontSize: 16
}copy
```
Every CSS property is defined as a separate property of the JavaScript object. Numeric values for pixels can be simply defined as integers. One of the major differences compared to regular CSS, is that hyphenated (kebab case) CSS properties are written in camelCase.

Next, we could add a "bottom block" to our application by creating a Footer component and defining the following inline styles for it:

```css
const Footer = () => {
  const footerStyle = {
    color: 'green',
    fontStyle: 'italic',
    fontSize: 16
  }
  return (
    <div style={footerStyle}>
      <br />
      <em>Note app, Department of Computer Science, University of Helsinki 2023</em>
    </div>
  )
}
```
```css
const App = () => {
  // ...

  return (
    <div>
      <h1>Notes</h1>

      <Notification message={errorMessage} />

      // ...  

      <Footer />
    </div>
  )
}
```