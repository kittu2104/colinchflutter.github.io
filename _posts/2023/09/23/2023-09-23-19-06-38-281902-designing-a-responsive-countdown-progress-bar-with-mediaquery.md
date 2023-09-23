---
layout: post
title: "Designing a responsive countdown progress bar with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [2ecc71, WebDesign, ResponsiveDesign]
comments: true
share: true
---

In today's blog post, we will explore how to create a responsive countdown progress bar using `MediaQuery` in CSS. This technique allows us to adapt our countdown progress bar to different screen sizes and ensure a seamless user experience across multiple devices.

## What is a Countdown Progress Bar?

A countdown progress bar is a visual representation that shows the remaining time for a particular event or task. It provides a clear indication of how much time is left until the event or task is completed.

## Using MediaQuery for Responsive Design

`MediaQuery` is a CSS feature that allows us to apply different styles based on the characteristics of the user's device, such as screen size, orientation, and resolution. By leveraging `MediaQuery`, we can ensure our countdown progress bar adapts to various screen sizes without sacrificing functionality.

## HTML Structure

Before we dive into the CSS, let's first set up the basic HTML structure for our countdown progress bar.

```html
<div class="countdown-bar">
  <div class="progress"></div>
</div>
```

## Styling the Countdown Progress Bar

Now let's add the CSS code to style our countdown progress bar. We will utilize `MediaQuery` to adjust the dimensions and appearance of the progress bar based on the screen size.

```css
/* Default styles */
.countdown-bar {
  width: 100%;
  height: 20px;
  background-color: #eee;
}

.progress {
  width: 0%;
  height: 100%;
  background-color: #2ecc71;
}

/* Responsive styles */
@media (max-width: 768px) {
  .countdown-bar {
    height: 10px;
  }
}
```

In the above example, we have set the default styles for the countdown bar with a height of 20 pixels and a background color of `#eee`. The `.progress` class represents the progress indicator and is initially set to 0% width.

Within the `@media` query, we have specified that for screen sizes smaller than or equal to 768 pixels, the height of the countdown bar should be reduced to 10 pixels. Feel free to adjust this value based on your requirements.

## Adding Countdown Functionality

To complete our countdown progress bar, we need to add JavaScript functionality to update the width of the progress indicator based on the remaining time. Below is an example code snippet using JavaScript.

```javascript
// Function to update the progress
function updateProgress(currentTime, totalTime) {
  const percentage = (currentTime / totalTime) * 100;
  document.querySelector('.progress').style.width = `${percentage}%`;
}

// Example usage
const totalTime = 10000; // Total time in milliseconds
let currentTime = 0; // Current time in milliseconds

setInterval(() => {
  currentTime += 1000; // Increment by 1 second
  updateProgress(currentTime, totalTime);
}, 1000);
```

In the above code snippet, we have created an `updateProgress()` function that calculates the percentage of time elapsed and updates the width of the progress indicator accordingly. We then use `setInterval()` to periodically update the progress every second.

## Conclusion

In this blog post, we have discussed how to design a responsive countdown progress bar using `MediaQuery` in CSS. By leveraging `MediaQuery`, we can ensure that our countdown progress bar adapts to different screen sizes, providing a consistent experience for users.

Remember to experiment with different styles and adapt the code to your specific requirements. With a well-designed countdown progress bar, you can enhance the user experience and effectively communicate the remaining time for any given event or task.

#WebDesign #ResponsiveDesign