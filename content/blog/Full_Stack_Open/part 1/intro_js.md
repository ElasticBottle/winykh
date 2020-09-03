---
title: "Introduction to JavaScript"
date: 2020-08-16T11:22:39+08:00
slug: "intro-js"
description: "the language of the web, now introduced"
keywords: ["Js", "JavaScript", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: true
---

## Variables

```js
let y = 5
const x = "Hello World"
```

Variables in JavaScript is dynamically typed.

Instead of `int`, `string`, we have `var`, `let`, and `const`.

In general, sticking to `const` and `let` is the safest.

`var` creates a variable whose scope is lifted up to as high as possible. Often, this is the global sate

`let` creates a variable with block scoping, people coming from java or c++ should be familiar with this.

`const` creates a variable that is prevented from being reassigned (we can still change values within array and objects)

Feel free to check out [this video](https://www.youtube.com/watch?v=sjyJBL5fkp8&feature=youtu.be) for more on `var`, `let`, and `const`.

### Variable types in JavaScript

- Number
- String
- Boolean
- Symbol (new in ES2015)
- Object
  - Function
  - Array
  - Date
  - RegExp
- null
- undefined

### Numbers

Just thought it would be an interesting fact, there's no such thing as an integer in JavaScript (except [BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)).

[`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) object provides some useful math related functions

## Equality matching

If you are coming from other programming background, know that `==` does not ensure that the type being compared have the same type.

```js
0 == '0' // true
```

To ensure that we get the expected behavior, use `===`. Add an extra `=` every where.

So `!=` becomes `!==` etc.

More on that topic [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

## Arrays

```js
const array = []
```

### Concat

`concat` creates a new list and adds the item to it

```js
const t = [1, -1, 3]
const t2 = t.concat(5)

console.log(t)  // [1, -1, 3] is printed
console.log(t2) // [1, -1, 3, 5] is printed
```

### Map

`map` create a a new list and return that new list after applying the function to all the elements

```js
const t = [1, 2, 3]

const m1 = t.map(value => value * 2)
console.log(m1)   // [2, 4, 6] is printed
```

### Reduce

`reduce` compresses a map down into a certain number of value.

```js
const t = [1,2, 3]

const sum = t.reduce((sum, value) => sum + value, 0)
```

Here, 0 is used as the initial value for `sum`, which can be any name you choose.

`value` is the particular element in the array.

The function is called through each element with the value of sum being brought forward each time.

### Filter

`filter` removes helps to pick an choose which elements in the array to keep base on certain conditions.

```js
const t = [1, 2, 5, ,6, 8, 9]
const smallNum = t.filter(num => num <== 5) //notice the ==, smallNum = [1, 2, 5]
```

### Destructing assignments

Use `...` to collect the remainder elements in an array

```js
const list = [1, ,2 ,3 , 4, 5]

const [one, two, ...remainder] = list // one = 1, two = 2, remainder = [3, ,4 ,5]
```

## Objects

```js
const object = {
    name: "John",
    age: 25
}

object["secret hobby"] = "badminton"
console.log(object.name) // prints John
```

Objects in JS are reminiscent of maps in other classes.

Accessing the keys can be done with the dot notation, square brackets can be used if the key has a space in the name.

In general, since they are prone to typo mistakes.

## Functions

Functions can be created the as in any other language

```js
function sum(a, b) {
  return a + b
}
```

Notice there is no return type, and instead a single `function` keyword, similar to `def` in python.

### Functions assigned to variables

Alternatively,functions can be created by assigning it to variables

```js
const sum = function(p1, p2) {
  console.log(p1)
  console.log(p2)
  return p1 + p2
}
```

Shorthand, `sum` can be written as:

```js
const sum = (p1, p2) => {
  console.log(p1)
  console.log(p2)
  return p1 + p2
}
const result = sum(1, 5) // prints 1, 5
console.log(result) // prints 6
```

Notice the use of `=>` and the dropping of the `function` keyword.

### Special function properties

With this assignment style functions, some interesting properties can be had.

Parenthesis for parameters can be dropped if there is only one parameters

```js
const square = p => {
  console.log(p)
  return p * p
}
```

Curly braces can be dropped for functions returning a single line of code

```js
const square = p => p * p
```

### The deal with `this`

Arrow functions and functions defined using the function keyword vary substantially when it comes to how they behave with respect to the keyword this, which refers to the object itself.

in Javascript the value of this is defined based on how the method is called. When calling the method through a reference the value of this becomes the so-called global object and the end result is often not what the software developer had originally intended.

Losing track of this when writing JavaScript code brings forth a few potential issues. Situations often arise where React or Node (or more specifically the JavaScript engine of the web browser) needs to call some method in an object that the developer has defined. However, in this course we avoid these issues by using the "this-less" JavaScript.

One situation leading to the "disappearance" of this arises when we set a timeout to call the greet function on the arto object, using the setTimeout function.

```js
const arto = {
  name: 'Arto Hellas',
  greet: function() {
    console.log('hello, my name is ' + this.name)
  },
}

setTimeout(arto.greet, 1000)
```

As mentioned, the value of this in JavaScript is defined based on how the method is being called. When setTimeout is calling the method, it is the JavaScript engine that actually calls the method and, at that point, this refers to the global object.

There are several mechanisms by which the original this can be preserved. One of these is using a method called bind:

```js
setTimeout(arto.greet.bind(arto), 1000)
```

Calling `arto.greet.bind(arto)` creates a new function where this is bound to point to `Arto`, independent of where and how the method is being called.

## Classes

There is no class mechanism like the ones in object-oriented programming languages. There are, however, features in JavaScript which make "simulating" object-oriented classes possible.

```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  greet() {
    console.log('hello, my name is ' + this.name)
  }
}

const adam = new Person('Adam Ondra', 35)
adam.greet()

const janja = new Person('Janja Garnbret', 22)
janja.greet()

```

At the core they are still objects based on [JavaScript's prototypal inheritance](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance).

The type of both objects is actually Object. JavaScript essentially only defines the types [Boolean, Null, Undefined, Number, String, Symbol, and Object.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

## Conclusion

That's all for this very short introduction to JavaScript, for a more in-depth dive, check out [A re-introduction to JavaScript by MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
