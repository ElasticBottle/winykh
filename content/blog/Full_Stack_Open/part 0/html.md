---
title: "Introduction to HTML"
date: 2020-08-08T11:22:39+08:00
slug: "intro-html"
description: "A short introduction to HTML"
keywords: ["Hypertext markup language", "HTML", "Web", "Web-dev"]
draft: false
tags: ["Full_Stack_Open", "Web"]
math: false
toc: false
---

HTML is a markup language that defines the structure of content in a webpage.

## Anatomy of an HTML Element

HTML consist of 3 parts:

- The tag (open and closing)
  - These include: `head, body, div, p, h1 through to h6, a, img`
  - Opening tags are simply surrounded by `<>` - `<head>`
  - closing tags include a `/` before the tag's name - `</head>`
- The attribute of the tag
  - Some common ones include `href, class, id`
- The content (some tags don't require content)

Together, these 3 elements form the an element of HTML.

```HTML
<p ATTRIBUTE_NAME = "ATTRIBUTE_VALUE"> The content </p>
```

## Nesting Elements

Tags are used to define a section of of content and therefore, it is totally possible to have them nested. 

That is, within a particular `div` tag, there can be multiple `p` tags.

The key thing is that tags must be closed in reverse order that they are open in.

```HTML
<div>
    <p>P tag, being opened last, is closed first</p>
</div>
```

## Content-less Elements

Some HTML elements do not require a content and one example is the `img` tag.

All `img` does is load an external resource into our website as the content.

```HTML
<img src="path_to_image" alt="descriptive text of image for assistive readers and people who cannot load image. Will be shown in place of image for the latter group">
```

## Structure of HTML Document

Below is a bare bones HTML document

```HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <img src="path_to_image" alt="descriptive text of image for assistive readers and people who cannot load image ">
  </body>
</html>
```

Some observations:

- `<!DOCTYPE html>`: Used to be included for error checks. Now, it's included for consistency and to ensure that everything works.
- `<html></html>`: The `<html>` element wraps the entire page. Sometimes called the root element.
- `<head></head>`: The `<head>` HTML element acts as a container for all metadata. This includes things like:
  - Keywords 
  - Page description for search results
  - CSS to style our content
  - Character set declarations and more.
-`<meta charset="utf-8">`: This element sets the character set your document should use to UTF-8. This character set includes most characters from the vast majority of written languages. There is no reason not to set this and it can help avoid some problems later on.
- `<title></title>`: The `<title>` element sets the title of your page. This is the text that appears in the browser tab and the title of the page when you bookmark/favorite it.
- `<body></body>` — The `<body>` element contains all the content that you want to show to others.

## Marking up text

### Headings

This are basically the title and subtitles you see in a book.

```HTML
<h1>Main title</h1>
<h2>Top level heading</h2>
<h3>Subheading</h3>
```

Do not use this as a way to style text, but rather, indicate the purpose of that particular text. This is because heading are used by assistive technologies and SEO.

Heading tags should be used in order. Use a `h3` only after a `h2` has been used. Not before.

### Paragraphs

The `<p>` tag is used to wrap a body of text

### Lists

There are two kinds of list:

- ordered
- unordered.

Their respective tags are `<ol>` and `<ul>`.

Individual elements in list are wrapped with `<li>`

```HTML
<ul> 
  <li>ordered</li>
  <li>unordered</li>
</ul>
```

### Links

Allows us to route to relevant pages.

We use the `<a>` tag, short for anchor tag to make this possible.

The href (short for Hypertext REFerence) attribute specify the page to link too.

```HTML
<a href="https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics">This page's reference resource</a>
```

## Conclusion

This covers the basics of HTML.

As noted in the links section, this introduction is a summary of the excellent write-up over at [firefox](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics).

For more, check-out [firefox's extensive write-ups](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML)

For any errors open an issue on this page's github repo.