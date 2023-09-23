---
layout: post
title: "Building a responsive collapsible panel with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [f1f1f1, HTML]
comments: true
share: true
---

In this tutorial, we will learn how to build a responsive collapsible panel using `MediaQuery` in HTML and CSS. This panel will automatically adjust its layout based on the screen size, making it ideal for websites and applications that need to be mobile-friendly.

## Requirements

To follow along with this tutorial, you will need:

1. HTML and CSS knowledge
2. An understanding of `MediaQuery`
3. A code editor (e.g., VS Code, Sublime Text, or Atom)

## Step 1: Setting up the HTML structure

Create an HTML file and open it in your code editor. Inside the `<body>` tag, add the following structure:

```html
<div class="panel">
  <div class="panel-header">Panel Header</div>
  <div class="panel-content">
    <p>This is the content of the panel.</p>
  </div>
</div>
```

In this example, we have a simple panel with a header and content section.

## Step 2: Styling the panel

To style the panel, we will use CSS. Open the CSS file and add the following styles:

```css
.panel {
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

.panel-header {
  background-color: #f1f1f1;
  padding: 10px;
  cursor: pointer;
}

.panel-content {
  padding: 10px;
  display: none;
}
```

These styles define the basic appearance of the panel, including its border, header, and content section.

## Step 3: Adding the collapsible functionality

To make the panel collapsible, we will use `MediaQuery` to detect the screen size and apply different CSS styles accordingly. Open the CSS file again and add the following styles:

```css
@media only screen and (max-width: 600px) {
  .panel-content {
    display: none;
  }
}

@media only screen and (min-width: 600px) {
  .panel-header {
    display: none;
  }
  .panel-content {
    display: block;
  }
}
```

In this example, we are using a media query to set different styles based on the screen width. When the screen size is below 600px, the content section is hidden. When the screen size is above 600px, the header is hidden, and the content section is displayed.

## Step 4: Test the collapsible panel

Save your changes and open the HTML file in a web browser. Now, when you resize the browser window, you should see the panel adjusting its layout according to the screen size.

## Conclusion

In this tutorial, we learned how to build a responsive collapsible panel using `MediaQuery` in HTML and CSS. By using media queries, we can create a panel that automatically adjusts its layout based on the screen size. This technique is essential for creating mobile-friendly websites and applications.

To summarize the steps:

1. Set up the HTML structure with a panel, header, and content sections.
2. Style the panel using CSS to define its appearance.
3. Use `MediaQuery` to add the collapsible functionality by applying different styles based on the screen size.
4. Test the panel by resizing the browser window and observing the responsive behavior.

Now you can apply this technique in your projects to enhance the user experience across different devices. Happy coding!

## #HTML #CSS