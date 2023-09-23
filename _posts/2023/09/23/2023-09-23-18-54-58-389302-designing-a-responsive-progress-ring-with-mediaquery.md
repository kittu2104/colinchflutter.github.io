---
layout: post
title: "Designing a responsive progress ring with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [webdevelopment, responsivedesign]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive progress ring using the `MediaQuery` class in CSS. The progress ring is a popular UI element used to visualize the progress of a task or the completion of a process.

## What is MediaQuery?

`MediaQuery` is a CSS class that allows us to apply different styles based on the characteristics of the device or browser being used to view the web page. It provides a way to make responsive designs by targeting specific screen sizes, resolutions, orientations, and other device properties.

## Creating the Progress Ring

To create a responsive progress ring, follow these steps:

### Step 1: HTML Markup

```html
<div class="progress-ring">
  <div class="progress-circle"></div>
  <div class="progress-text">50%</div>
</div>
```

In this example, we have a container div with the class "progress-ring" that will hold our progress ring element. Inside the container, we have two child divs: one for the progress circle (with the class "progress-circle") and one for the progress text (with the class "progress-text").

### Step 2: CSS Styling

```css
/* Set initial styles */
.progress-ring {
  position: relative;
  width: 200px;
  height: 200px;
}

.progress-circle {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background-color: lightgray;
}

.progress-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 24px;
  font-weight: bold;
  color: black;
}

/* Apply responsive styles */
@media (max-width: 768px) {
  .progress-ring {
    width: 150px;
    height: 150px;
  }

  .progress-text {
    font-size: 18px;
  }
}
```

In the above CSS code, we first set the initial styles for the progress ring and its child elements. The progress ring container has a fixed width and height of 200 pixels. The progress circle is positioned absolutely within the container and given a light gray background. The progress text is positioned at the center of the container and styled with a 24px font size and bold weight.

Then, we apply responsive styles using the `@media` rule. This rule targets devices with a maximum width of 768 pixels (e.g., tablets and mobile devices). Inside the media query, we adjust the width and height of the progress ring container to 150 pixels and decrease the font size of the progress text to 18 pixels.

## Usage

To use the responsive progress ring in your own project, simply copy and paste the HTML markup and CSS code provided above. You can customize the styles as per your requirements.

## Conclusion

By using `MediaQuery` in CSS, we can easily create a responsive progress ring that adapts to different screen sizes and device characteristics. This allows us to provide a better user experience and ensure that our UI elements are displayed correctly across various devices.

#webdevelopment #responsivedesign