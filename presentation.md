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

In a typical web application, you have 3 layers:

* .highlight[**Data Layer**] - Stores the data of the application (Users, posts, comments, etc...)
* .highlight[**Logical Layer**] - Manages the interactions between the View Layer and the Data Layer (An HTTP API for example)
* .highlight[**View Layer**] - The page that is visible to users and with which they can interact

React should only be used in the .highlight[**View Layer**].
