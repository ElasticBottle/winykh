---
title: "States in React"
date: 2020-08-19T11:22:39+08:00
slug: "states-in-react"
description: "An introduction to managing states in react"
keywords: ["Web Forms", "forms", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: true
---

Before we dive into handling states in react, let's look at some helpful tricks that build on our knowledge of [react](intro_react.md) and [JavaScript](intro_js.md).

In particular, [destructing](#destructing), [helper functions](#helper-functions), and [event handling](#event-handling)

## Destructing

We briefly touched on destructing back in the [short introduction to JavaScript](intro_js.md).

Here's a refresher:

```js
const list = [1, 2, 3, ,4 5]
const [first, second, ..rest]  = list
```

Notice that square brackets surround the variables, and the "rest" pattern is at the end.

The same can apply when destructing objects, but instead of square brackets, we use curly braces.

```js
const Component = (props) => {
    const {name, age} = props
    return <div>
        <p> name </p>
        <p> age </p>
    </div>
}
```

Of course, this can be taken one step further and have the destructing right in the parameters as follows:

```js
const Component = ({name, age}) => {
    return <div>
        <p> name </p>
        <p> age </p>
    </div>
}
```

This way, we reduce the amount of boilerplate code that we need to write. Yay! :smile:

## Helper Functions

Sometimes, a component require help before it can display the data.

When that happens, it can be useful to declare a helper functions to handle the logic before passing the final result to be rendered.

```js
cart = [
    item1: {
        price: 10.
        desc: '...'
    },
    item12: {
        price: 20.
        desc: '...'
    },
    ...
]
const Total = ({cart}) {
    const totalCost = (cart) => {
        let cost = 0
        for (const item of cart) {
            cost += item.price
        }
        return cost
    }
    return <p> Total cost: ${totalCost(cart)}</p>
}
```

Here, we defined a simple function that sums the cost of the items in an array.

You can start to see how it keeps our code neater as the complexity of component increases.

## Event Handling

Event Handling is a process of registering functions to be called when specific events occur. Clicking is a common example.

Here is how a button click is registered in react:

```js
const Counter = () => {
  const increment = () => console.log('clicked')

  return <div>
        <div>{counter}</div>
        <button onClick={increment}>
            plus
        </button>
        <button onClick={() => console.log('clicked')}>
            minus
        </button>
    </div>
}

const App = () => {
  return (
    <Counter />
  )
}
```

The main area of interest is `<button onClick={increment}>`. Here, `onClick` takes a function.

It is possible to declare the function directly in the onClick attribute, as in:

```js
<button onClick={() => console.log('clicked')}>
```

This is not recommended. Again, because things can get complicated fast.

Read more about [event handling in react docs](https://reactjs.org/docs/handling-events.html)

### Function in Functions

Functions returning functions can be utilized in defining generic functionality that can be customized with parameters.

```js
const hello = (who) => () => {
  console.log('hello', who)
}
<button onClick={hello("John")}>Say hello to John</button>
```

Of course, the same can be achieved without functions in functions.

```js
const hello = who => console.log('hello', who)
<button onClick={() => hello('John')}>Say hello to John</button>
```

Choosing which approach is merely a matter of preference.

## Stateful Components in React using Hooks

Up till now, all the components that we have looked at in react are static.

What does it mean?

The value of the component never changes throughout the lifecycle.

However, sometimes, we do want values of component to change depending on the circumstances.

That is where stateful components come into play.

```js
import {userState} from 'react'
import ReactDOM from 'react-dom'

const Counter = () => {
  const [counter, setCounter] = useState(0)
  setTimeout(() => setCounter(counter + 1), 1000)
  return <p>
    {counter}
  </p>
}

const App = () => {
   return <Counter />
}

ReactDOM.render(<App />, document.getElementById('root'))
```

Some Observations:

- `import {userState} from 'react'`: Imports the `userState` function for creating stateful components
- `const [counter, setCounter] = useState(0)`: Creates a stateful element with initial value of 0
  - `userState` returns an array containing:
    - Initial value of the state
    - A function to update the value of the state
  - This is the creation of our react hook
- `setTimeout(function, time)`: executes `function` after `time` milliseconds.
  - In this case, `setCounter` the update state function is called after 1 seconds (1000 milliseconds). `counter` is then set to the new value in `setCounter`.

When the component is re-rendered, the body of the component is re-executed, thereby creating a perpetual cycle of updates.

[State in react docs.](https://reactjs.org/docs/state-and-lifecycle.html)

## Managing Complex States

The above is a simple example of state in react.

Often though, there are multiple states to be managed.

In that case, it is as simple as defining multiple `useState()`.

```js
const App = (props) => {
  const [left, setLeft] = useState(0)
  const [right, setRight] = useState(0)
  const [allClicks, setAll] = useState([])

  const incrementLeft = () => {
    setAll(allClicks.concat('L'))
    setLeft (left + 1)
  }

  const incrementRight = () => {
    setAll(allClicks.concat('R'))
    setRight(right + 1)
  }

  return (
    <div>
      <div>
        {clicks.left}
        <button onClick={incrementLeft}>left</button>
        <button onClick={incrementRight}>right</button>
        {clicks.right}
      </div>
      <p>{allClicks.join(' ')}</p>
    </div>
  )
}
```

Some Observations:

- `setAll(allClicks.concat('R'))` is used to update the state of the array instead of `.push('R')`. This is because we want to preserve state immutability (more on that later)
- `<p>{allClicks.join(' ')}</p>` joins each element in `allClicks` separated by a space. This is the inverse behavior from python's `join` if you are coming from there.

Sometimes, it might be beneficial to have states stored together in an object.

When would you want this?

When the state changes are related to each other in some way.

Finally, remember that *state in react should no be mutated*! Never modify the states directly. This is the same principle as in not directly modifying `props` in components.

Why?

To prevent unwanted side effects. Like thinking a variable should have one value only to have it contain another due to mutation.

Instead, create new copies of the state to be assigned via the react hooks (`setLeft` / `setRight`).

## Rules of Hooks

The `useState` function should only be called inside a function body that defines a React Component.

It must not be called from inside of a loop, a conditional expression, or any place that is not a function defining a component.

Why?

To ensure that the hooks are always called in the same order, and if this isn't the case, the application will behave erratically.

## State among multiple Components: Lifting State update

Having covered States and its complexities, we can now turn our attention to how to manage the same states across multiple components.

To manage such a scenario, it is important that the state resides in the component directly parent to all the components requiring shared state.

```js
const Display = ({ value }) => {
  return <p> {value} </p>
}

const Button = ({ handleChange, text }) => {
  return <button onClick={handleChange}>
    {text}
  </button>
}

const Counter = () => {
  const [counter, setCounter] = useState(0)

  const increment = () => setCounter(counter + 1)
  const decrement = () => setCounter(counter - 1)

  return <div>
    <Display value={counter} />
    <Button handleChange={increment} text="plus" />
    <Button handleChange={decrement} text="minus" />
  </div>
}
```

Some Observations:

- `Counter` is the master Component, managing the state across `Display` and `Button`.
- `Display` and `Button` all maintain the same state of `counter` (note, it's lower case 'c', and not `Counter`)

For more lifting states up, [react docs](https://reactjs.org/docs/lifting-state-up.html) is a good place.

## Conditional Rendering in React

At times, we want to render different elements base on the state that the users are in.

In that case, simply use conditional rendering.

```js
const History = (props) => {
  if (props.allClicks.length === 0) {
    return (
      <div>
        the app is used by pressing the buttons
      </div>
    )
  }

  return (
    <div>
      button press history: {props.allClicks.join(' ')}
    </div>
  )
}
```

Conditional Rendering is a big topic in of itself. [Check the docs](https://reactjs.org/docs/conditional-rendering.html) for more.
