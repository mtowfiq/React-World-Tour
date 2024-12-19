Milestone 7:
**************************************************
1) React Core Concepts (part-1)

- ReactJS is a JS library for building UI.

- It breaks web elements into reusable components.

- Components are basically building blocks, which are merged together to form a UI.

- A react component is a JS function that you can sprinkle with markup except:
1) Their names always begin with a capital letter
2) They return JSX markup (or easier HTML markup)

- JSX stands for JS XML and lets you write HTML-like markup inside a JS file. Under the hood it's transformed into regular JS using compilers like Typescript.

- JSX isnt supported by browsers (as browsers can only render HTML, CSS, and JS). To enable a browser to read JSX, we need to transform it to a regular JS using compiler like Babel and then pass it to the browser.

- Rules of JSX:
1) Return a single root element. (for eg div). To return multiple elements from a component, wrap them with a single parent tag or fragment (aka empty tag).

2) Close all the tags (for eg img tag)

3) Use camelCase

- Use className instead of class for adding classes.

- Another way of adding styles is by creating an object consisting of css styles in camelcase. Then using the style attribute.

function Developer(){
  const developerStyle = {
    margin: "20px",
    padding: "20px",
    border: "2px solid purple",
    borderRadius: "20px"
  }
  return(
    <div style={developerStyle}>
      <h5>Yada Yada</h5>
      <p>IDK</p>
    </div>
  )
}

OR

function Developer(){
  return(
    <div style={{
    margin: "20px",
    padding: "20px",
    border: "2px solid purple",
    borderRadius: "20px"
  }}>
      <h5>Yada Yada</h5>
      <p>IDK</p>
    </div>
  )
}

- To display data dynamically we use props. The component that we have created, can take any property of our wish and can take any value (in the markup), and to get those values we need to pass that property as "prop" as an argument to that component function. This prop is the object name and contains the property/key and value we have set in the markup.

- Since we get an object in the argument, we can destructure it there. We can set default values while destructuring as well. 

<Device name="Watch" price="20"></Device>

function Device({name = "IDK", price = 0}){
  console.log(name, price)
  return <h2>This device: {name} and the price is {price}</h2>
}

- Props are used to send data from one component to another. To pass props, add them to the JSX just like you would with HTML attributes. Props are immutable (meaning they cant be changed when accessed). In this example we are sending data from the app component to our own made components.
Below from the app component we are sending data to device, student components, and those components are accepting an argument in the form of props which are essentially objects.

function App() {

  return (
    <>
      <h1>Vite + React</h1>
      <Device name="Laptop" price="55"></Device>
      <Device name="Phone" price="17"></Device>
      <Device name="Watch" price="20"></Device>
      <Person></Person>
      <Student></Student>
      <Developer></Developer>
    </>
  )
}

- If we want to pass a number or boolean as the value of a prop key then use {number or boolean value}.

- ^ (continuation of previous point) Basically passing anything other than strings, we need to pass inside {}.

- We cant change the value of props inside the component as it's read-only. However, if we destructure it, it makes another variable which can be changed.

- When we create a component in another file and want to use somewhere else, we need to export that component and import it in the file we want to use.

export default function Todo({task}){
    return (
        <li>Task: {task}</li>
    )
}

import Todo from "./todo";

- Conditional rendering: 
1)) Option 1: Using if-else

export default function Todo({task, isDone}){
    if(isDone){
        return <li>Finished: {task}</li>
    }
    else{
        return <li>Work on: {task}</li>
    }
}

2)) Using only if. Since boolean can take only two values true and false, if it satisfies the condition then do one thing, if not just do the other thing (we dont need to explicitly state else).

export default function Todo({task, isDone}){
    if(isDone){
        return <li>Finished: {task}</li>
    }
    return <li>Work on: {task}</li>
}

3)) Using ternary operator

export default function Todo({task, isDone}){
//     return(
//         <li>{isDone ? "Finished": "Work on"} : {task}</li>
//     )
}

4)) Using and operator. If the left side is true then execute the right side.

export default function Todo({task, isDone}){
    return (
        <li>{task} : {isDone && " Done"}</li>
    )
}

5)) Using or operator. If the left side is false, then execute the right side.

export default function Todo({task, isDone}){
    return(
        <li>{task} {isDone || ": Work on it"}</li>
    )
}

6)) Using if-else and setting the html to a variable and returning it, instead of directly returning the html.

export default function Todo({task, isDone}){
    let listItem;
    if(isDone){
        listItem = <li>Finished : {task}</li>
    }
    else{
        listItem = <li>Work on : {task}</li>
    }
    return listItem
}


- If we have an array or array of objects, and we want to use those elements in the array and send it as props to components, then use { } along with the map function. Below are examples-

function App() {
  const actors = ["Tom", "Cruise", "Holland", "Brad Pitt"];
  const singers = [
    {id: 1, name: "JB", age: 30},
    {id: 2, name: "Bruno", age: 35},
    {id: 3, name: "PM", age: 37},
    {id: 4, name: "Doja", age: 28}
  ]
  return (
      {
        singers.map(singer => <Singer singer = {singer}></Singer>)
      }
      <Actor name={"Thawfiq"}></Actor>
      {
        actors.map(actor => <Actor name = {actor}></Actor>)
      }
  )

}

export default function Singer({singer}){
    console.log(singer)
    return(
        <div>
            <h3>Singer: {singer.name}</h3>
            <p>Age: {singer.age}</p>
        </div>
    )
}

export default function Actor({name}){
    return <li>Name: {name}</li>
}

- We can pass an array (or an array of objects) as props as well. In the component, we recieve an array and can use array methods like .length as well.

  const books = [
    {id: 1, name: "physics", price: 100},
    {id: 2, name: "maths", price: 120},
    {id: 3, name: "chem", price: 140},
    {id: 4, name: "english", price: 150}

  ]

  function App(){
    return(
      <>
        <BookStore books={books}></BookStore>
      </>
    )
  }

  export default function BookStore({books}){
    return(
        <>
            <h3>Books: {books.length}</h3>
        </>
    )
}

- We can send props from the root component to a component (component-1-bookstore) and use another component (component-2-book) in the first component.

<!-- We created an array of object and passed it to the BookStore component as props (passed the entire array as a whole) -->
  function App(){
    const books = [
    {id: 1, name: "physics", price: 100},
    {id: 2, name: "maths", price: 120},
    {id: 3, name: "chem", price: 140},
    {id: 4, name: "english", price: 150}

  ]
    return(
      <>
        <BookStore books={books}></BookStore>
      </>
    )
  }

<!-- In the BookStore component we recieved the array and we dynamically traversed trhough each element of the array using map function and inside it we used another component called Book to which we pass each element of the array -->
import Book from "./Book"
export default function BookStore({books}){
    return(
        <>
            <h3>Books: {books.length}</h3>
            {
                books.map(book => <Book book={book}></Book>)
            }
        </>
    )
}

<!-- In the Book component, we recieve every single elements of the array, and return something.  -->
import './book.css';
export default function Book({book}){
    return(
        <div className='book'>
            <h3>Book Name: {book.name}</h3>
        </div>
    )
}


**************************************************
2) React Core Concepts (part-2)

- In React, do handle events, there are few changes we need to make as opposed to just HTML and JS.
In HTML and JS, it was something like-

<button onclick="handleClick()">CLick me</button>

function handleClick(){
  alert("Clicked);
}

But in React, we use onClick (with C capital) and we dont use quotation mark instead we use curly brackets, also we dont call the function, we just use the function name.

1) Using normal function
  function App(){
    function handleClick(){
      alert("CLicked")
    }
    return(
      <button onClick={handleClick}>Click me using normal function</button>
    )
  
  }

2) Using arrow function

function App(){
    const handleClick2 = () => alert("Clicked 2")
    return(
      <button onClick={handleClick2}>Click me using arrow function</button>
    )
  
  }

3) On the onclick attribute itself 

function App(){
    return(
      <button onClick={() => alert("Third click")}>Click me using arrow function directly on onClick</button>
    )
  
  }


- UseState returns an array where the first element is a number or any text or boolean, and the second is a function which updates the existing value.
The variable (the first element is accessible inside the component). Basically using the function we update the existing value.

- We use states when there's a possiblity of something to change, and we want to manage that change and display it on the UI.

- A component with add and reduce buttons-

import { useState } from "react"

export default function Counter(){
    const [count, setCount] = useState(0)

    const handleAdd = () =>{
        const newCount = count + 1
        setCount(newCount)
    }
    const handleReduce = () =>{
        const newcount = count - 1
        setCount(newcount)
    }
    return(
        <div style={{border: "2px solid yellow"}}>
            <h3>Counter: {count}</h3>
            <button onClick={handleAdd}>Add</button>
            <button onClick={handleReduce}>Reduce</button>
        </div>
    )
}

- If somethings starts with "use", then it's a react hook

- useEffect exists to synchronize a component with an external system (like fetching data). 

- Code for basic use of useEffect-

import { useEffect, useState } from "react"

export default function Users(){
    const [users, setUsers] = useState([])
    // Used empty array as the initial value, as from the api we're getting an array of object, which is essentially an array. The api maybe broken, so firts we initialize it to an empty array, and when it'ssuccessfully fetched, then we update it.


    useEffect(()=>{
        fetch("https://jsonplaceholder.typicode.com/users")
        .then(res => res.json())
        .then(data => setUsers(data))
    },[])
    // The second paramater is the dependency array, and here it's an empty array which means it will run only once (we need to fetch the data only once).
    return(
        <div>
            <h3>Users: {users.length}</h3>
        </div>
    )
}

- If we didnt use useEffect in the code above, and just used fetch-then, then there would be an infinite loop, as when the state changes, there would be a trigger and that would cause it to fetch the api again.

- Rendering means that react is calling your component, which is a function.
Any screen update in a react app happens in 3 steps:
1) Trigger - triggers when state changes
2) Render - after triggering, react calls your component to figure out what to display on screen.
3) Commit - displays to the dom

- Side effects one example is fetching data.

- Similar in look, different in data - thinking in react way.















**************************************************
3) Simple React Rest Countries

- There's a VS code extension called "React Extension Pack", and this allow us to quickly get the structure of a component by just writing 'rsc' + tab. 

- If there are more than 7-8 components it's best to keep them in a folder under src. Also, if there's a possibility of the components having seperate css file, then create a folder for that component and css file seperately, under that folder.

- When we use a component multiple times (like 100s) dynamically (using map function), then react gives us a warning to use "key" props. The value of it will be something unique. This is so that the code is optimized and can be handled efficiently. 

    return (
        <div>
            <h3>Countries: {countries.length}</h3>
            {
                countries.map(country => <Country key={country.cca3} country = {country}></Country>)
            }
        </div>
    );

- We sometimes might get a warning- prop types eslint warning. Here when we are sending props, it's a good idea to validate or mention the type of prop data we are sending. It can be turned off from eslintrc.cjs file.


























































**************************************************
4) 