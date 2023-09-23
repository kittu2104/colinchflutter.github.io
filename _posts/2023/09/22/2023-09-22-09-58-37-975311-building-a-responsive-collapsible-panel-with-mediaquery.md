---
layout: post
title: "Building a responsive collapsible panel with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [f5f5f5, webdevelopment]
comments: true
share: true
---

In this tutorial, I will show you how to build a responsive collapsible panel using **MediaQuery** in your web development project.

## What is MediaQuery?
**MediaQuery** is a CSS feature that allows you to apply different styles to your website based on the characteristics of the device being used to view it. This includes features such as screen size, device orientation, and more. By leveraging MediaQuery, we can create dynamic and responsive layouts.

## Getting Started
To get started, let's create a basic HTML structure for our collapsible panel:

```html
<div class="collapsible-panel">
    <div class="panel-header">
        <h3>Click to Collapse</h3>
    </div>
    <div class="panel-content">
        <p>This is the content of the panel.</p>
    </div>
</div>
```

## CSS Styling
Now, let's apply some CSS styling to create a collapsible panel with a toggle effect:

```css
.collapsible-panel {
    border: 1px solid #ddd;
}
.panel-header {
    background-color: #f5f5f5;
    padding: 10px;
    cursor: pointer;
}
.panel-content {
    padding: 10px;
    display: none;
}
```
In the CSS code above, we set the basic structure of our panel with a border, header, and content. Initially, we hide the panel content by setting its display property to none.

## Adding JavaScript Functionality
To make the panel collapsible, we will use JavaScript to add interactivity. Here's an example of how you can achieve this:

```javascript
const panelHeader = document.querySelector('.panel-header');
const panelContent = document.querySelector('.panel-content');

panelHeader.addEventListener('click', function() {
    if (panelContent.style.display === 'none') {
        panelContent.style.display = 'block';
    } else {
        panelContent.style.display = 'none';
    }
});
```

In the JavaScript code above, we select the panel header and content elements using their respective classes. We then add an event listener to the panel header, which toggles the display property of the panel content when clicked.

## Making the Panel Responsive
Now let's make our collapsible panel responsive using **MediaQuery**. We will modify the CSS to change the panel layout on different screen sizes. Here's an example:

```css
@media screen and (max-width: 768px) {
    .collapsible-panel {
        width: 100%;
        margin-bottom: 10px;
    }
}
```

In the CSS code above, we use a **MediaQuery** with a `max-width` value of 768 pixels. Inside this MediaQuery, we adjust the width and add a margin-bottom to the collapsible panel, making it responsive.

## Conclusion
By incorporating **MediaQuery** into our web development project, we can create a responsive collapsible panel that adapts to different screen sizes. This can greatly enhance the user experience and make our website more accessible across various devices.

Feel free to customize the panel styling and JavaScript functionality further to suit your project needs. Let me know if you have any questions or need further assistance!

#webdevelopment #responsivedesign