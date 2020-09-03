---
title: "Tips For Debugging React Apps"
date: 2020-08-20T11:22:39+08:00
slug: "debug-react"
description: "developer console is your friend"
keywords: ["debugging react apps", "react troubleshooting", "Web", "Web-dev"]
draft: false
tags: ["Full Stack Open", "Web"]
math: false
toc: false
---

## Use the developer console

It is the first place that gets notified when anything goes wrong should anything goes wrong.

## Add `debugger` for line breaks

This will cause the app to stop running at that particular line, allowing us to inspect the elements and variables at that point in time.

Alternatively, break points can be added in the source tab under the developer's console.

## Separate Object and string values with comma in `console.log`

```js
console.log('props value is', props)
```

This way, both the string and the contents of the variable will be printed.

The wrong way would be to use `+`. In which case the class of the Object is simply printed.

## Grab the react Chrome extension

[The extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) adds a new tab to the developer console.

Using the extension gives us an easy way to inspect the various react components and their `state` and `props`
