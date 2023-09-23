---
layout: post
title: "Designing a responsive page indicator with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [webdevelopment, responsivedesign]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive page indicator using the `MediaQuery` feature in CSS. The page indicator will dynamically adjust its width and number of pages displayed based on the screen size of the device.

## Requirements
Before we start, make sure you have a basic understanding of HTML and CSS.

## Step 1: Set up the HTML Structure
First, let's set up the HTML structure for our page indicator. We'll use a `<ul>` element to create a list of pages.

```html
<ul class="page-indicator">
  <li class="page active"></li>
  <li class="page"></li>
  <li class="page"></li>
  <li class="page"></li>
</ul>
```

## Step 2: Style the Page Indicator
Now, let's add some CSS to style the page indicator. We'll position the pages horizontally, add a background color, and define their dimensions.

```css
.page-indicator {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.page {
  width: 20px;
  height: 10px;
  margin-right: 10px;
  background-color: #ccc;
}

.page.active {
  background-color: #333;
}
```

## Step 3: Add Responsive Styling with MediaQuery
To make our page indicator responsive, we'll use `MediaQuery` to apply different styles for different screen sizes.

```css
@media (max-width: 600px) {
  .page {
    width: 15px;
    height: 8px;
    margin-right: 8px;
  }
}

@media (max-width: 400px) {
  .page {
    width: 10px;
    height: 6px;
    margin-right: 6px;
  }
}
```

In the above code, we use `@media` to specify different styles for screens with a maximum width of 600px and 400px respectively.

## Step 4: Test and Adjust
Now, open your HTML file in a web browser and resize the window to see the responsive page indicator in action. The page indicator will automatically adjust its size and spacing based on the screen width.

## Conclusion
By using `MediaQuery` in CSS, we were able to create a responsive page indicator that adapts to different screen sizes. This technique can be useful in building responsive web pages and applications.

#webdevelopment #responsivedesign