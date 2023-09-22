---
layout: post
title: "Designing a responsive horizontal stepper with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [e0e0e0, 55aaff]
comments: true
share: true
---

In this blog post, we will explore how to design a responsive horizontal stepper using `MediaQuery` in order to create a seamless user experience across different devices and screen sizes.

## What is a Horizontal Stepper?

A horizontal stepper is a user interface component that guides users through a multi-step process. It is commonly used in forms, onboarding flows, or any situation where a task needs to be broken down into multiple steps.

## Why Responsive Design Matters

With the increasing usage of mobile devices, it is crucial to design user interfaces that adapt to different screen sizes. Responsive design ensures that your horizontal stepper looks and functions well regardless of the device being used. By utilizing `MediaQuery`, we can create a dynamic layout that adjusts based on screen size.

## Implementing a Responsive Horizontal Stepper

To begin with, we need to structure our HTML markup to represent the different steps in our horizontal stepper. Each step can be represented by a `div` element with a unique identifier.

```html
<div id="step1">Step 1</div>
<div id="step2">Step 2</div>
<div id="step3">Step 3</div>
```

Next, let's define the CSS styles for our horizontal stepper. We will use flexbox to create a horizontal layout.

```css
.stepper-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.stepper-step {
  flex: 1;
  padding: 10px;
  text-align: center;
}

/* Additional styles for active and completed steps */
.stepper-step.active {
  background-color: #e0e0e0;
}

.stepper-step.completed {
  background-color: #55aaff;
  color: white;
}
```

Now, let's add the JavaScript logic to handle the responsiveness using `MediaQuery`. We can use the `window.matchMedia` method to check the screen width and apply appropriate styles.

```javascript
const mediaQuery = window.matchMedia('(max-width: 600px)');

function handleScreenChange(e) {
  if (e.matches) {
    // Apply styles for small screens
    document.querySelector('.stepper-container').classList.add('small-screen');
  } else {
    // Remove styles for small screens
    document.querySelector('.stepper-container').classList.remove('small-screen');
  }
}

mediaQuery.addListener(handleScreenChange); // Attach listener on screen change
handleScreenChange(mediaQuery); // Initially check screen width

```

Finally, we need to update our CSS to handle the responsive layout.

```css
.stepper-container.small-screen {
  flex-direction: column;
}

.stepper-step {
  /* Adjust styles for small screens */
}

/* Additional styles for active and completed steps in small screens */
.stepper-step.active {
  /* Adjust background color */
}

.stepper-step.completed {
  /* Adjust background color */
  /* Adjust text color */
}
```

By applying the above CSS styles, the horizontal stepper will adapt and stack vertically on small screens, providing a better user experience.

## Conclusion

In this blog post, we have explored how to design a responsive horizontal stepper using `MediaQuery`. By utilizing `MediaQuery`, we can create a dynamic layout that adapts to different screen sizes, providing a seamless user experience. Implementing a responsive design is vital in today's mobile-dominated world to ensure your user interface looks and functions well across various devices.

#techblog #responsivedesign