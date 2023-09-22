---
layout: post
title: "Designing a responsive stepper slider with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [design, responsive]
comments: true
share: true
---

In this tutorial, we will learn how to design a responsive stepper slider using `MediaQuery` in CSS. This will allow us to create a slider that adjusts its layout and behavior based on the device's screen size.

Before we dive into the implementation, let's define what a stepper slider is. A stepper slider is a component that displays a series of steps or slides, allowing users to navigate through them by either clicking on the individual steps or using previous and next buttons.

### HTML Markup

To begin, let's set up our HTML markup for the stepper slider:

```html
<div class="slider">
  <div class="step">Step 1</div>
  <div class="step">Step 2</div>
  <div class="step">Step 3</div>
  <div class="step">Step 4</div>
  <div class="step">Step 5</div>
</div>
```

In this example, we have a container with a class of "slider" that wraps the individual steps, each represented by a div with a class of "step".

### CSS Styles

Now, let's add some CSS styles to create the stepper slider:

```css
.slider {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.step {
  flex: 1;
  padding: 1rem;
  background-color: lightgray;
  text-align: center;
}
```

In this CSS code, we set `display: flex` on the slider container to create a horizontal layout for the steps. We use `justify-content: space-between` to distribute the steps evenly and add some gap between them using `gap: 1rem`.

The `.step` class styles each step, giving it a flexible width of `flex: 1` to distribute the available space evenly. We also add some padding, a background color, and center align the text within each step.

### Responsive Layout

To make the stepper slider responsive, we can use `MediaQuery` in CSS to apply different styling for different screen sizes. Let's update our CSS code to include responsive styles:

```css
@media screen and (max-width: 768px) {
  .slider {
    flex-direction: column;
  }
  
  .step {
    width: auto;
  }
}
```

In this example, we target screens with a maximum width of 768 pixels. For screens of this size or smaller, we change the `flex-direction` of the `.slider` container to `column`, stacking the steps vertically. We also set the width of each step to `auto`, allowing them to take up the full width of the container.

### Final Thoughts

By using `MediaQuery` in CSS, we can create a responsive stepper slider that adjusts its layout and behavior based on the device's screen size. This allows us to provide an optimal user experience across different devices.

Remember to test your slider on various devices and screen sizes to ensure it behaves as expected. Don't forget to `#design` and `#responsive` when sharing your creation!

Happy coding!