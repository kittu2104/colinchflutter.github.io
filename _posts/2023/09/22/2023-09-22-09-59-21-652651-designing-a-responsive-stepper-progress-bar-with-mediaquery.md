---
layout: post
title: "Designing a responsive stepper progress bar with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [responsive, stepper]
comments: true
share: true
---

A stepper progress bar is a great way to visually represent multi-step processes or forms. It allows users to keep track of their progress and lets them know how many steps are left to complete. In this tutorial, we will show you how to create a responsive stepper progress bar using CSS Media Queries.

## Prerequisites
To follow along with this tutorial, you will need basic knowledge of HTML, CSS, and Javascript.

## Step 1: Set Up HTML Structure
Let's start by setting up the HTML structure for our stepper progress bar. We will use an unordered list (`<ul>`) with list items (`<li>`) for each step:

```html
<ul class="stepper">
  <li>Step 1</li>
  <li>Step 2</li>
  <li>Step 3</li>
  <li>Step 4</li>
</ul>
```

## Step 2: Styling the Stepper
Next, let's add some CSS to style our stepper progress bar. We'll use flexbox to align the list items horizontally and apply some basic styling:

```css
.stepper {
  display: flex;
  justify-content: space-between;
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.stepper li {
  flex: 1;
  text-align: center;
  font-weight: bold;
  padding: 10px;
  background-color: #ddd;
  color: #555;
}
```

## Step 3: Responsive Stepper with Media Queries
Now let's make our stepper progress bar responsive using CSS Media Queries. We'll define different styles for different screen sizes. For example, on smaller screens, we'll change the flex direction to vertical and increase the font size:

```css
@media only screen and (max-width: 600px) {
  .stepper {
    flex-direction: column;
  }

  .stepper li {
    font-size: 16px;
  }
}
```

## Step 4: Test and Adjust
Finally, test your stepper progress bar on different devices and screen sizes to ensure it looks and functions as expected. Make any necessary adjustments to the CSS based on your testing results.

## Conclusion

By using CSS Media Queries, we can easily create a responsive stepper progress bar that adapts to different screen sizes. This allows for a better user experience across various devices. Experiment with different CSS styles and breakpoints to customize the look and feel of your stepper progress bar.

#responsive #stepper