---
layout: post
title: "Building a responsive file picker with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [selectedFile, f2f2f2, webdevelopment, javascript]
comments: true
share: true
---

In today's digital world, file handling and management has become an essential part of many web applications. One common feature needed for file management is a file picker, which allows users to select files from their devices. In this tutorial, we will learn how to build a responsive file picker using the `MediaQuery` class in combination with HTML and CSS.

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of HTML, CSS, and JavaScript.

## Step 1: Setting up the HTML

Start by creating a basic HTML structure with the necessary elements for the file picker:

```html
<input type="file" id="filePicker" />
<div id="selectedFile"></div>
```

In the above code, we have an input element of type `file` with the id `filePicker` and a `<div>` element with the id `selectedFile` to display the selected file.

## Step 2: Adding CSS styling

Let's add some CSS to style our file picker:

```css
#selectedFile {
  padding: 10px;
  background-color: #f2f2f2;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-top: 10px;
}
```

The above CSS will give a simple styling to the `selectedFile` div.

## Step 3: Handling file selection with JavaScript

Now, let's write JavaScript code to handle file selection and display the selected file's name:

```javascript
const filePicker = document.getElementById('filePicker');
const selectedFile = document.getElementById('selectedFile');

filePicker.addEventListener('change', (event) => {
  const fileName = event.target.files[0].name;
  selectedFile.textContent = `Selected file: ${fileName}`;
});
```

In the above code, we listen for changes in the file picker using the `change` event and retrieve the selected file's name from the `event.target.files` object. We then update the `selectedFile` div's text content to display the selected file's name.

## Step 4: Making the file picker responsive

To make the file picker responsive, we can utilize the `MediaQuery` class from JavaScript:

```javascript
const mediaQuery = window.matchMedia('(max-width: 600px)');

function handleResponsiveChanges(mediaQuery) {
  if (mediaQuery.matches) {
    filePicker.setAttribute('accept', 'image/*');
  } else {
    filePicker.removeAttribute('accept');
  }
}

mediaQuery.addEventListener('change', handleResponsiveChanges);
handleResponsiveChanges(mediaQuery);
```

In the above code, we create a `MediaQuery` object with a condition for a maximum width of 600 pixels. The `handleResponsiveChanges` function is triggered whenever the status of the media query matches change. Inside the function, we conditionally set or remove the `accept` attribute of the file picker based on whether the media query matches or not.

## Conclusion

By using the `MediaQuery` class, we can easily create a responsive file picker that adapts to different screen sizes. This allows for a better user experience and ensures your web application is accessible across various devices.

#webdevelopment #javascript