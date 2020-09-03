---
title: "Introduction to CSS"
date: 2020-08-10T11:22:39+08:00
slug: "intro-css"
description: "A short introduction to css"
keywords: ["Cascading Style Sheets", "CSS", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: false
---

CSS, short of Cascading style sheets, is a style sheet language.

CSS is what you use to selectively style HTML elements.

## Setting up CSS with HTML

To have our css be applied to a particular page, we need to include a link to the css file in the `<head>` of the html document.

```html
<head>
    ...
    ...
    ...
    <link href="styles/style.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
</head>
```

Here, we added our own style sheet along with google's OpenSans font that we can use. 

## Anatomy of CSS document

```css
h1 {
    color: blue;
}
```

Some observations:

- **The selector**: `h1` defines the element that is affected by our styling
- **The Declaration**: `color: blue;` contains:
  - **Property**: 'color', the particular property that you want to be styled
  - **Property value**: 'blue' the value for a given property

Each declaration is a key-value pair. This means that the **Property** and **Property value** is separated by a `:`

Each declaration ends with `;`

## Selecting elements

### Multiple Elements

Multiple elements can be selected at once for a given rule-set. Simply separate elements with a comma.

```css
h1, p, li {
  color: blue;
}
```

### Invalid Elements

Invalid elements will result in the group set it belongs too be ignored.

### Types of element Selectors

| Type of selector                 | Example                                                          | Description                                                                                                                           |
| -------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Tag                              | `h1 {}`                                                          | Selects element base on their tag                                                                                                     |
| Class                            | `.class_name {}`                                                 | Prefixed with period(`.`). Selects element base on the value of the `class` attribute                                                 |
| ID                               | `#id_value {}`                                                   | Prefixed with `#`. Selects element base on the value of the `id` attribute                                                            |
| Attribute                        | `img[src] {}`, `a[href = 'link']`                                | Selects elements of those tags with the particular attribute name and/or name with value                                              |
| Pseudo-class and pseudo-elements | `a:hover{}`, `p:first-child{}`, `p::first-line{}`, `p::before{}` | Pseudo-class has one `:` while pseudo-elements have two `::` separating tag name and pseudo-class\element name.                       |
| Combinators                      | `div > p {}`, `div p {}`                                         | Selects in parent order. The first selects all the `p` who are children of `div`. The second selects `p` who are descendants of `div` |

Check out [MDN Selectors guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors) for more on selecting elements.

## Styling elements

Each css element can be thought of as a box.

The box has:

- **Padding**: The space around the content.
- **border**: The solid line around the padding.
- **margin**: The space around the outside of the border.

An example styling can be as such:
```css
body {
  margin: 0 auto; /*vertical | horizontal, auto means that available space is evenly distributed, in this case, between left and right*/
  padding: 0 20px 20px 20px; /*Top | Left | Bottom | Right*/
  border: 5px solid black; /*Border Width | Style | Border Color*/
  width: 600px; /* Size of the content in pixels*/

  background-color: #FF9500;
  color: #00539F; /*Often text of children // content */

  text-align: center;
  text-shadow: 3px 3px 1px black; /*Horizontal | Vertical | Blur factor | Blur color*/
  
  font-family: "Open Sans", sans-serif; /* this should be the rest of the output you got from Google fonts */
  font-size: 10px;
  line-height: 2;
  letter-spacing: 1px;
}
```

And that's it! When to use what is an intuition that builds over time from styling html over and over again.

Read more about [margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin#Syntax) or [padding](https://developer.mozilla.org/en-US/docs/Web/CSS/padding#Syntax).

## Conclusion

As with the previous note on [HTML](../part%200/html.md), this summary is built off the amazing write-up over at [Mozilla's Developer Network](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)