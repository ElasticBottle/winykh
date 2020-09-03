---
title: "Introduction to React"
date: 2020-08-17T11:22:39+08:00
slug: "intro-react"
description: "An Introduction to React"
keywords: ["React", "forms", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: true
---

React is a library developed by Facebook to enable building of webpages with reusable widgets.

A core philosophy of React is composing applications from many specialized reusable components.

For this introduction, we'll be exploring a bare bones react code:

```js
import React from 'react'
import ReactDOM from 'react-dom'

const App = () => (
  <div>
    <p>Hello world</p>
  </div>
)

ReactDOM.render(<App />, document.getElementById('root'))
```

## JSX: The markup language of choice for React

The `<div>` tags might look awfully similar to HTML, but in reality, it is JSX, a syntax extension to JavaScript.

JSX is "XML-like", which means that every tag needs to be closed. For example, a newline in HTML can be written as `<br>`, but when writing JSX, the tag needs to be closed, `<br />`.

## Component

A component in react is a *javascript function* that *returns a single DOM element*.

In this case, `App` is a react component. A strong convention in react is having `App` as the root in the component tree for the react application.

### Composing with components

Always start component names with a capital letter.

React treats components starting with lowercase letters as DOM tags. For example, `<div />` represents an HTML div tag, but `<HelloWorld />` represents a component and requires `HelloWorld` to be in scope.

Also, do not define components within components. Things get messy quickly when components are nested within other components. it makes debugging harder.

```js
const HelloWorld = (props) => (
    <p>
        Hello World
    </p>
)

const App = () => (
  <div>
    <HelloWorld />
  </div>
)
```

`props`, short for properties, is the only argument a component accept. (More on that [later](#props-passing-data-to-components)) All React components must act like pure functions with respect to their props. In other words, the component *must never modify its own props*.

Sometimes, we would like to avoid adding unnecessary nodes to the DOM, This can be avoided by using fragments, which are basically an empty element:

```js
const App = () => (
  <>
    <HelloWorld />
  </>
)
```

For more on [fragments](https://reactjs.org/docs/fragments.html#short-syntax)

### props: passing data to components

Data is passed by having attributes in the JSX element, similar to HTML

A React component reads all value into a map of sorts called `props`, short for properties.

```js
const HelloWorld = (props) => (
    <p>
        Hello {props.name}
    </p>
)

const App = () => {
    const name = "Johnny
    <div>
        <HelloWorld name = "John"/>
        <HelloWorld name = {name} />
    </div>
}
```

There can be an arbitrary number of props, passing JS variables require wrapping the variable name in curly braces

For an attribute, quotes (for string values) or curly braces (for expressions) are fine, but not both in a single attribute
