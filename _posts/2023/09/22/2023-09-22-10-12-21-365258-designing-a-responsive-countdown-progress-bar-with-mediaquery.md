---
layout: post
title: "Designing a responsive countdown progress bar with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [f2f2f2, 4caf50]
comments: true
share: true
---

![Responsive Countdown Progress Bar](countdown-progress-bar.png)

Are you looking for an engaging way to display a countdown progress bar on your website? A responsive countdown progress bar can add an element of anticipation and keep your users engaged. In this tutorial, we will explore how to design and implement a responsive countdown progress bar using `MediaQuery`.

## What is `MediaQuery`?

`MediaQuery` is a powerful feature in CSS that allows you to apply different styles based on the characteristics of the user's device or viewport. By using media queries, you can create responsive designs that adapt to different screen sizes and orientations.

## HTML Markup

```html
<div class="countdown-container">
  <div class="progress-bar"></div>
</div>
```

To begin, we need a simple HTML structure. We have a container element for the countdown progress bar and inside it, we have the progress bar itself.

## CSS Styling

Now, let's apply some CSS styling to our countdown progress bar.

```css
.countdown-container {
  width: 100%;
  height: 30px;
  background-color: #f2f2f2;
  border-radius: 5px;
  overflow: hidden;
}

.progress-bar {
  width: 0%;
  height: 100%;
  background-color: #4caf50;
  transition: width 1s linear;
}
```

Here, we set the width and height of the container and progress bar elements. We also define the background color and border radius for the container, and the background color for the progress bar. The `transition` property is used to create a smooth animation effect when the progress bar width changes.

## JavaScript Function

Next, we will create a JavaScript function to update the width of the progress bar based on the remaining time.

```javascript
function updateProgressBar() {
  const countdownContainer = document.querySelector('.countdown-container');
  const progressBar = document.querySelector('.progress-bar');

  const countdownSeconds = 60; // Change this value to adjust the countdown time
  const remainingSeconds = countdownSeconds - (countdownSeconds * progressBar.offsetWidth) / countdownContainer.offsetWidth;

  progressBar.style.width = `${(remainingSeconds / countdownSeconds) * 100}%`;

  setTimeout(updateProgressBar, 1000);
}

// Call the function when the page loads
window.addEventListener('load', updateProgressBar);
```

In this JavaScript function, we first select the countdown container and progress bar elements using `querySelector`. We then calculate the remaining time in seconds by subtracting the percentage width of the progress bar from the total countdown seconds. We update the width of the progress bar based on the remaining time. Finally, we call the `updateProgressBar` function using `setTimeout` to continuously update the progress bar every second.

## Making it Responsive with `MediaQuery`

To make our countdown progress bar responsive, we can use `MediaQuery` to adjust its size and appearance for different screen sizes.

```css
@media (max-width: 600px) {
  .countdown-container {
    height: 20px;
  }
}

@media (max-width: 400px) {
  .countdown-container {
    height: 15px;
  }
  .progress-bar {
    background-color: #db4437;
  }
}
```

Here, we define media queries for different screen widths. In the first media query, when the screen width is less than or equal to 600px, we reduce the height of the countdown container. In the second media query, when the screen width is less than or equal to 400px, we further reduce the countdown container height and change the background color of the progress bar to a different color.

## Conclusion

By leveraging the power of `MediaQuery`, we have successfully designed a responsive countdown progress bar. This progress bar will adapt its size and appearance based on the user's device or viewport, creating a seamless user experience across different screen sizes. Experiment with different styles, colors, and countdown times to make it fit your website design. Happy coding!

#ResponsiveDesign #CountdownProgressBar