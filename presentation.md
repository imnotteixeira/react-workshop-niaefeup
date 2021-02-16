class: center, middle, inverse, small-images

# React
## Declaring UI instead of handling every state change manually
![](./img/ni_logo.png)

##### 17 Feb 2021

---
class: inverse

# Will this be a boring workshop?

### No.

.highlight[Please feel free to interrupt and ask questions, make this more of a conversation and less of a lecture.]

What we have on menu today:
1. What is React exactly
1. React Theory
1. Common libraries that go well together with React
1. React in practice

---
class: inverse

# Your Host

<div class="left" style="display: flex; align-items: center; gap: 1em">
<div><img width=150 src="./img/angelo.jpg" style="display: inline-block; border-radius: 50%"/></div>
<div>
    <p class="highlight">Angelo Teixeira</p>
    <p>MIEIC Finalist</p>
    <p>2+ Years experience with React - Including internships and NIJobs</p>
</div>
</div>

<!-- Use this if you have more presenters -->
<!-- <div class="right" style="display: flex; align-items: center; gap: 1em;justify-content: flex-end">
<div>
    <p class="highlight">Second Host</p>
</div>
<div><img width=150 src="./img/img-name" style="display: inline-block; border-radius: 50%"/></div> -->

</div>



---
class: center, middle, inverse

# React
## What is it, really?

---

# React

.highlight[React] is a .highlight[JavaScript] library that automatically renders and handles component updates on a `<div>` of your website 

.center[
```javascript
ReactDOM.render(
    <App />,
    document.getElementById("root")
);
```
]

---

# React

This allows it to run .highlight[wherever] inside an existing website. You can even migrate progressively from old UIs to React-powered UI components. 

React is just glorified JavaScript. Always keep this in mind! To use it, you just need to load it in a `script` tag in your HTML, then you can use all of its functionalities.

---

# React in an HTML page

.center[
```html
<html lang="en">
    <head>
        <meta charset="utf-8">
        <title>NIJobs</title>
        <link href="https://ni.fe.up.pt/st4g1ng/nijobs/static/css/main.4f9a2d8f.chunk.css" rel="stylesheet">
    </head>
    <body>
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <div id="root"></div>

        <!-- React source code -->
        <script src="https://ni.fe.up.pt/st4g1ng/nijobs/static/js/2.8ac0d13b.chunk.js"></script>
        <!-- Application source code, using React -->
        <script src="https://ni.fe.up.pt/st4g1ng/nijobs/static/js/main.df8d00d7.chunk.js"></script>
    </body>
</html>
```
]

---

# React vs JavaScript

React .highlight[**is**] JavaScript. Most of the problems you'll face are just JavaScript problems.

In fact, React was really good in the sense that it made me learn a lot of JavaScript theory.

---

# React is only the View

<!-- In a typical web application, you have 3 layers: -->

* .highlight[**Data Layer**] - Stores the data of the application (Users, posts, comments, etc...)
* .highlight[**Logical Layer**] - Manages the interactions between the View Layer and the Data Layer (An HTTP API for example)
* .highlight[**View Layer**] - The page that is visible to users and with which they can interact

###### React is designed to only be used in the .highlight[**View Layer**].

.height-limit-250[![MVC Pattern](./img/web-mvc.png)]

---
class: middle

# Declaratve vs Imperative Paradigms


In .highlight[Imperative] programming, you define exactly what will be done and .highlight[how].

In .highlight[Declarative] programming, you define what happens depending on some state.

---

# Imperative Programming

.center[
```javascript
function markSelected(id) {
    const item = document.getElementById(id);
    item.classList.add("selected");
}

Array.from(document.getElementsByClassName("todo-item"))
    .forEach(elem => elem.addEventListener("click", markSelected(elem.id)))

```
]

---

# Declarative Programming (in React)

.center[
```javascript

const [items, setItems] = useState([{isSelected: false, text: "TODO1"}])

const toggleItemSelection = (i) => {
    setItems((items) => {
        const updatedItems = cloneDeep(items);
        updatedItems[i].isSelected = !items[i].isSelected
        return updatedItems
    });
}

items.map((item, i) => (
    <p 
        className={item.isSelected && "selected"}
        onClick={toggleItemSelection(i)}
    >
        {item.text}
    </p>
))
```
]

---

# Comparison

Declarative has a big advantage since it releases you from needing to think how things interact with each other every time.

If you ever wanted to add a "how many are selected" counter in the previous example, in the imperative version, you needed to add a new listener or change the current one. In the declarative version, you just need a new component that counts the items which have `isSelected: true`, since that is already done in the onClick definition of the item.

Think about the state and how it changes, not how the components change. The components will change according to the current state automatically*.

##### * Of course you still need to link the state to the component in some way for it to know about it, like we do by using the `isSelected` variable

---

# Context Sum up

* React is not a website maker.
* There are no "React websites". There are websites that *use* React.
* This is why React is a library and not a framework.
* React uses declarative programming to design the interface components, making them rely on a state, instead of requiring you to specify exactly how they should modify themselves. React handles the DOM changes for you :)

---

class: center, middle, inverse

# React Theory

## Now it will start to make sense, I hope

---

# JSX

React uses an HTML-in-JS language (JSX) that lets you specify the components similarly to how you would do it in regular HTML. There are some differences like using `className` instead of `class`, and allowing you to have JavaScript sections to generate some parts of it

.center[
```html
<div className="meteorolgy-widget">
<p>{"This is Javascript. " + "Today it's " + getMeteoPrediction()}</p>
{
    weeklyPredictions.map(prediction => (
        <p>{prediction.day + " - " + prediction.state}</p>
    ))
}
</div>
```
]

---

# Components

React is based on a tree of components it will recursively render. A component can render none or multiple children, which will be other components, which will be rendered themselves, and so on.

It is generally a good practice to create small and simple components and leave each component responsible for the minimum logic possible.

.center[
```javascript
const NewsWebpage = ({news, ads}) => (
    <> // Special "dummy" component - React.Fragment
        <NewsArea news={news}/>
        <AdsColumn ads={ads}>
    </>
)
```
]

---

# Components - Props

In order to change dynamically, Components can receive a `props` object to use when creating the rendering logic.

Components always have a `children` prop representing their children components.

---
# Components - Props


.center.dense-wide[
```html
const WrapperThatAddsAnHelloV1 = (props) => (
    <>
        <p>Hello,</p>
        <p>{props.name}</p>
    </>
)

const WrapperThatAddsAnHelloV2 = (props) => (
    <>
        <p>Hello,</p>
        {props.children}
    </>
)

const MyPage = () => (
    <>
        <WrapperThatAddsAnHelloV1 name="World"/>
        <WrapperThatAddsAnHelloV2>
            <p>World</p>
        </WrapperThatAddsAnHelloV2>
    </>
)
```
]

---

# DOM and VDOM

DOM (Document Object Model) is the browser's representation of a web page.

```html
<html>
    <head>
      <title>DOM</title>
    </head> 
    <body>
        <p>Hello World</p>
    </body>
</html>
```

React has the concept of the .highlight[Virtual DOM], which it stores internally to manage the components' state.

---

# VDOM

Virtual DOM enables some optimizations when rendering the components in the browser (reconciliation phase), as it only updates the relevant components instead of the whole page.

#### Reconciliation Phase

When the VDOM changes are mapped to instructions to update the real DOM (append, delete and update operations). These instructions are generated by comparing the new version of the VDOM with the older one, and generating the minimum set of operations required to change it on the DOM.

This is a known problem for which state-of-the-art algorithms have a complexity in the order of O(n^3), n being the number of tree elements.

---

# Reconciliation Optimizations

If we used this in React, displaying 1000 elements would require in the order of one billion comparisons. This is far too expensive. Instead, React implements a heuristic O(n) algorithm based on two assumptions:

* Two elements of different types will produce different trees.
* The developer can hint at which child elements may be stable across different renders with a key prop.

---

# Reconciliating Lists

By default, when recursing on the children of a DOM node, React just iterates over both lists of children at the same time and generates a mutation whenever there’s a difference.

For example, when adding an element at the end of the children, converting between these two trees works well:

.dense[
```html
<ul> <!-- before -->
  <li>first</li>
  <li>second</li>
</ul>
<ul> <!-- after -->
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```
]
React will match the two `<li>first</li>` trees, match the two `<li>second</li>` trees, and then insert the `<li>third</li>` tree.

---

# Reconciliating Lists

If you implement it naively, inserting an element at the beginning has worse performance. For example, converting between these two trees works poorly:

.dense[
```html
<ul> <!-- before -->
  <li>Duke</li>
  <li>Villanova</li>
</ul>
<ul><!-- after -->
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```
]

React will mutate every child instead of realizing it can keep the `<li>Duke</li>` and `<li>Villanova</li>` subtrees intact. This inefficiency can be a problem.

---

# Keys

In order to solve this issue, React supports a key attribute. When children have keys, React uses the key to match children in the original tree with children in the subsequent tree. For example, adding a key to our inefficient example above can make the tree conversion efficient:

.dense[
```html
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
```
]

Now React knows that the element with key '2014' is the new one, and the elements with the keys '2015' and '2016' have just moved.

---

# Keys

Usually, react will let you know when you have some list of mutating children and you should be using keys. 

But there are some things to consider before choosing your keys:

* They must be unique among the elements of the same list
* They must be constant during the life of the element on the list

---

# Keys

A first instinct is to use array indexes as keys, since they are obviously unique among elements.

However, they don't respect the second rule if the list changes with some reorder, for example.

<br>
<br>

Let's check an example...

https://jsbin.com/gotihihihi/edit?js,output

---

# Component Lifecycle

In order to interact with the Virtual DOM, React lets you use React Components, which can be classes or functions (we’ll use functions) that represent a part of the website and can contain more components inside them.

These React Components are bound by a Lifecycle that manages their existence and interactions, which reflect on the actual DOM after the .highlight[Reconciliation Phase].

---

# Component Lifecycle

There are 4 steps:

* .highlight[**Mounting**] (When the component is first added to the DOM): 
    * The methods and events that take place here happen as the component is mounted in the DOM.
* .highlight[**Updating**] (When the state or one of the props change, or if parent re-renders*): 
    * Here the methods and events take place after the React component has entered the DOM.
* .highlight[**Un-mounting**]: 
    * Here the methods and events take place as they React component leaves the DOM or is unmounted from the DOM.
* .highlight[**Error Boundaries**]: 
    * This is a special category that deals with handling or gracefully catching errors in order not to totally break your React application render.


###### * Might not happen if the child component is memoized with React.memo(), for example

---

# React Hooks

React .highlight[Hooks] are JavaScript .highlight[functions] that can interact with the component, by executing specific actions during the component lifecycle.

React exposes some default hooks, but you can create custom hooks which call React's ones for more complex scenarios.

There are two rules when using React Hooks:

* Only Call Hooks at the Top Level. 
    * Don’t call Hooks inside loops, conditions, or nested functions. Instead, always use Hooks at the top level of your React function.
* Only Call Hooks from React Functions. Don’t call Hooks from regular JavaScript functions. Instead, you can:
    * Call Hooks from React function components.
    * Call Hooks from custom Hooks

---

# Common React Hooks

### useState(initialState)
Let's you store some state in-between re-renders. If you pass a function as the initial value, it will only run it on the first render.

Returns an array where the first value is the state value and the second is a setter function for that value.

It's recommended you have a separate state for every variable you want to store, instead of a giant object with a field for each.

.dense[
```javascript
const [count, setCount] = useState(0);

const incrementCounter = () => {
    setCount(count + 1)
}

const decrementCounter = () => {
    setCount(currentCount => currentCount - 1)
}
```
]

---

# Common React Hooks

### useState(initialState)

##### `setState(val)` vs `setState(fn)`

Using functional version is better due to async updates. If you call `incrementCounter` in rapid succession, React will batch the updates and race conditions may prevent the counter from updating multiple times, i.e. the `count` variable will not update in between calls.

Using an updater function, the "current state" variable is always correct.

---

# Common React Hooks

### useEffect(fn, [...dependencies])

Lets you execute code at different stages of the lifecycle. It is called at every render, but it might do nothing, depending on the dependencies.

```javascript
useEffect(() => {
    // This will run on every render
})
```

Notice the .highlight[undefined] dependency array. This is the same as not calling `useEffect`, and writing the code directly on the component.

---

# Common React Hooks

### useEffect(fn, [...dependencies])

```javascript
useEffect(() => {
    // This will run on mount only
}, [])
```

Notice the .highlight[empty] dependency array.

---

# Common React Hooks

### useEffect(fn, [...dependencies])

```javascript
useEffect(() => {
    // This will run every time the dependencies change
    console.log(foo, bar)
}, [foo, bar])

```
`foo` and `bar` might be some component props or variables created inside the component that depend on props. If the props change, making `foo` or `bar` change, the `useEffect` function will be executed.

Does not execute if the .highlight[references] to the dependencies don’t change

---

# Common React Hooks

### useRef(initialValue)

`useRef` is similar to `useState`, however it does not trigger anything on change. It's just a mutable JavaScript object with a current field which stores whatever.

It's also used to store references to DOM elements, so that you can program something .highlight[imperatively], if needed.

.dense[
```javascript
function TextInputWithFocusButton() {
    const inputEl = useRef(null);
    const onButtonClick = () => {
        // `current` points to the mounted text input element
        inputEl.current.focus();
    };
    return (
        <>
            <input ref={inputEl} type="text" />
            <button onClick={onButtonClick}>Focus the input</button>
        </>
    );
}
```
]

---
class: center, middle, inverse

# Common Patterns
## Don't re-invent the wheel

---

# Controller Component

A component that handles all the state and only renders stateless components to handle the visual part.

---

# Controller Component

.dense[
```html
const FormHandler = () => {
    const [name, setName] = useState("")
    const [age, setAge] = useState(0)

    const handleSubmit = () => //call something using `name` and `age`

    return (
        <form onSubmit={handleSubmit}>
            <input 
                value={name} 
                onChange={(e) => setName(e.target.value)}
            />
            <input 
                type="number"
                value={age} 
                onChange={(e) => setAge(e.target.value)}
            />
            <button type="submit">
                </form>
    )
}
```
]

---

# Higher-order Component (HoC)

A function that wraps components to inject some props

.dense[
```html
// Utils file
const withMath = (WrappedComponent) => {
    const sum = (a,b) => a+b

    return (
        <WrappedComponent sum={sum} />
    )
}

// Component file
const MyCalculator = ({sum, a, b}) => (
    <div>
        <input value={a}/>
        <input value={b}/>
        <button onClick={sum(a,b)}>Sum</button>
    </div>
)

export default withMath(MyCalculator);
// No need to specify the sum `prop` when using this component. It will already be populated by the `withMath()`.

```

]

