---
layout: post
title: "Designing a responsive stepper timeline with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [007bff, 28a745]
comments: true
share: true
---

In today's tech-savvy world, responsive web design has become a necessity. A responsive design adapts to different devices and screen sizes, ensuring optimal user experience. One common component that can be found in many websites and applications is a stepper timeline - a visual representation of a process or sequential steps. In this blog post, we will explore how to design a responsive stepper timeline using the `MediaQuery` feature in CSS.

## Step 1: HTML Markup
Let's start by creating the HTML markup for our stepper timeline. We will use an unordered list (`<ul>`) to represent each step, with list items (`<li>`) as the individual steps. Here's an example:

```html
<ul class="stepper">
    <li>Step 1</li>
    <li>Step 2</li>
    <li>Step 3</li>
    <li>Step 4</li>
    <li>Step 5</li>
</ul>
```

## Step 2: CSS Styling
Next, we will style the stepper timeline using CSS. We will use flexbox to create a horizontal layout and align the steps accordingly. Here's an example:

```css
.stepper {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.stepper li {
    list-style: none;
    padding: 10px;
    background-color: #ccc;
    color: #fff;
    font-weight: bold;
}

/* Additional styling for active and completed steps */
.stepper li.active {
    background-color: #007bff;
}

.stepper li.completed {
    background-color: #28a745;
}
```

## Step 3: Making it Responsive with MediaQuery
To make our stepper timeline responsive, we will use `MediaQuery` to apply different styles based on the screen size. For smaller screens, we will switch to a vertical layout for better readability. Here's an example:

```css
/* Apply different styles for screens smaller than 768px */
@media screen and (max-width: 768px) {
    .stepper {
        flex-direction: column;
        align-items: flex-start;
    }
    
    .stepper li {
        margin-bottom: 10px;
    }
}
```

## Conclusion
By combining HTML, CSS, and `MediaQuery`, we can design a responsive stepper timeline that provides an optimal user experience across various devices and screen sizes. The use of `MediaQuery` allows us to adapt the layout and styling based on different screen dimensions. Experiment with different styles and customize it to match your project's requirements.

#WebDesign #ResponsiveDesign