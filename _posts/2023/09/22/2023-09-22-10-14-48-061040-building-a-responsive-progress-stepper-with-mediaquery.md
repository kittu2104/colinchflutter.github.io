---
layout: post
title: "Building a responsive progress stepper with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [webdevelopment, responsivedesign]
comments: true
share: true
---

Progress steppers are a common UI element used to guide users through a multi-step process. They provide a visual indication of the user's progress and help them understand how much more they need to complete. In this blog post, we will explore how to build a responsive progress stepper using `MediaQuery` in CSS.

## Setting Up the HTML Markup

First, let's set up the HTML markup for our progress stepper. We will use an unordered list (`<ul>`) with list items (`<li>`) representing each step of the process. Each list item will contain a label and a circle as the visual indicator.

```html
<ul class="progress-stepper">
  <li>
    <span class="label">Step 1</span>
    <div class="circle"></div>
  </li>
  <li>
    <span class="label">Step 2</span>
    <div class="circle"></div>
  </li>
  <li>
    <span class="label">Step 3</span>
    <div class="circle"></div>
  </li>
</ul>
```

## Styling the Progress Stepper

Next, let's style the progress stepper using CSS. We will use flexbox to align the list items horizontally and add a border to the circles to resemble the stepper. We will also use `MediaQuery` to make the stepper responsive.

```css
.progress-stepper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.label {
  text-align: center;
  margin-bottom: 5px;
}

.circle {
  width: 30px;
  height: 30px;
  border: 2px solid #000;
  border-radius: 50%;
}

@media (max-width: 767px) {
  .progress-stepper {
    flex-wrap: wrap;
  }
  
  .circle {
    margin-bottom: 10px;
  }
}
```
In the above CSS, we have defined a media query `@media (max-width: 767px)` to apply specific styles when the viewport width is less than or equal to 767 pixels. Inside the media query, we have added `flex-wrap: wrap` to allow the list items to wrap to the next line and increased the margin bottom of the circles to give extra vertical spacing on smaller screens.

## Conclusion

In this blog post, we learned how to build a responsive progress stepper using `MediaQuery` in CSS. By using media queries, we can easily adjust the styling of our progress stepper based on different viewport sizes. This ensures that our progress stepper remains user-friendly and visually appealing on various devices.

#webdevelopment #responsivedesign