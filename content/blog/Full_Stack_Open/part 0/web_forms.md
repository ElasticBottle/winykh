---
title: "Introduction to Web Forms"
date: 2020-08-11T11:22:39+08:00
slug: "intro-web-forms"
description: "A short introduction to web forms"
keywords: ["Web Forms", "forms", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: false
---

Web forms are one of the main ways a user interacts with a web site or application.

Form controls can also be programmed to validate values entered and paired with text labels that describe their purpose to both sighted and blind users.

If you are looking for a [short introduction to HTML](../part%200/html.md) instead.

## Designing Forms

From a user experience (UX) point of view, the bigger your form, the more you risk losing users. Ask only what you absolutely need. For more, check out [smashing Magazine's article on UX](https://www.smashingmagazine.com/2018/08/ux-html5-mobile-form-part-1/)

## Implementing a form

All forms start with a `<form>` element, like this:

```HTML
<form action="/my-handling-form-page" method="post">

</form>
```

The `<form>` element is like a `<section>` or `<footer>` element, but specifically for containing forms.

Some common attributes of a form:

- `action`: Defines the URL to send the form's data when form is submitted
- `method`: Defines the HTTP method to send the data with (usually `get` or `post`)

### Adding text fields

Adding to our form element.

```HTML
<ul>
    <li>
        <label for="name">Name:</label>
        <input type="text" id="name" name="name">
    </li>
    <li>
        <label for="email">E-mail:</label>
        <input type="email" id="email" name="email">
    </li>
    <li>
        <label for="msg">Message:</label>
        <textarea id="msg" name="user_message">Some default text</textarea>
    </li>
    <li class="button">
        <button type="submit">Send your message</button>
    </li>
</ul>
 ```

- `<li>`: Help makes styling easier (see later in the article). 
- `<label>`: The text label.
  - Notice the `for` attribute which takes the id of the form widget it is associated with.
  - This enables user to click on the label to activate the corresponding form widget, and it also provides an accessible name for assistive readers.
- `<input>`: The point of interaction between user and the web application.
  - `type` attribute specifies how the `<input>` element appears and behaves.
    - some common `type` attribute includes: `file`, `password`, `checkbox`, `radio`, `email`, and `text`.
  - `value`: specifies the initial value.
  - `name`: The associated key when submitting data for The particular form's input value.
- `<textarea>`: A freeform text area. Notice the closing tag.
  - Default values are specified in between the open and close tags
- `<button>`: `type` attribute accepts one of three values: `submit`, `reset`, or `button`.
  - `submit` is the default value for the `type` attribute.
    - Sends the form's data to the URL specified by `action` in the `<form>` element
  - `reset` - should not be used since it erases all the user's work so far and reverts the form back to its original state. This in itself can be done by refreshing the page if the user really wants anyways.
  - `button` does nothing, but allows for custom functionality through javaScript

### Styling forms

This article won't be going into the details of styling, but an example style for the form above can be found [here](https://github.com/mdn/learning-area/blob/master/html/forms/your-first-HTML-form/first-form-styled.html)

Check out the [intro to css article](css.md) for more.
