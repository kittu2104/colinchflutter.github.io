---
layout: post
title: "Designing a responsive stepper progress bar with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [e0e0e0, 4caf50, webdevelopment, responsivedesign]
comments: true
share: true
---

In modern web and mobile applications, it is common to have multi-step forms or processes that require users to move through a series of steps. A progress bar can be a useful visual indicator to show users their progress and how much more they need to complete.

In this tutorial, we will design a responsive stepper progress bar using the `MediaQuery` feature in CSS. This allows us to adjust the layout and appearance of the progress bar based on different screen sizes and devices.

## Step 1: HTML Markup

First, let's create the basic HTML structure for our stepper progress bar. We will use an unordered list (`<ul>`) to represent the steps, and each step will be an `<li>` element. We will also add a class to mark the current active step.

```html
<ul class="progress-bar">
  <li class="active">Step 1</li>
  <li>Step 2</li>
  <li>Step 3</li>
  <li>Step 4</li>
</ul>
```

## Step 2: CSS Styling

Next, let's add the CSS styles to create the stepper progress bar. We will use `flexbox` to align the steps horizontally and apply styles to indicate the progress.

```css
.progress-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.progress-bar li {
  flex-grow: 1;
  text-align: center;
  list-style-type: none;
  padding: 10px;
  background-color: #e0e0e0;
  color: #aaa;
}

.progress-bar li.active {
  background-color: #4caf50;
  color: #fff;
}
```

## Step 3: Responsive Design with `MediaQuery`

To make our stepper progress bar responsive, we will use `MediaQuery` to change the layout and appearance based on different screen sizes. For example, on smaller screens, we might want to stack the steps vertically instead of horizontally.

```css
@media (max-width: 600px) {
  .progress-bar {
    flex-direction: column;
  }

  .progress-bar li {
    margin-bottom: 10px;
  }
}
```

In this example, the `max-width` of `600px` triggers the `MediaQuery`, and the `flex-direction` property changes the flow of the steps to vertical. We also add some margin between the steps to improve readability.

## Step 4: Testing

To test our responsive stepper progress bar, open the HTML file in a web browser and adjust the browser width to see how the layout and appearance of the progress bar change based on the defined `MediaQuery`.

## Conclusion

In this tutorial, we have designed a responsive stepper progress bar using `MediaQuery` in CSS. By using `MediaQuery`, we can customize the layout and appearance of the progress bar to adapt to different screen sizes and devices. This helps create a better user experience for applications with multi-step processes. Give it a try in your own projects and enhance the usability of your forms or processes.

#webdevelopment #responsivedesign