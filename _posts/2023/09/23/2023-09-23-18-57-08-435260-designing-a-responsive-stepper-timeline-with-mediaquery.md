---
layout: post
title: "Designing a responsive stepper timeline with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [stepper, stepper, stepper, webdevelopment, responsivedesign]
comments: true
share: true
---

In modern web development, creating responsive and interactive user interfaces is crucial. One common UI element is a stepper timeline, which allows users to navigate through different steps or stages of a process. In this tutorial, we will learn how to create a responsive stepper timeline using `MediaQuery` in CSS.

## Prerequisites
To follow along with this tutorial, you should have a basic understanding of HTML, CSS, and JavaScript.

## Step 1: Setting up the HTML structure
First, let's set up the basic HTML structure for our stepper timeline. We'll start with a `<div>` element with a unique ID to act as a container for our timeline. Inside this container, we'll create several `<div>` elements to represent each step of the timeline.

```html
<div id="stepper">
  <div class="step active">Step 1</div>
  <div class="step">Step 2</div>
  <div class="step">Step 3</div>
  <div class="step">Step 4</div>
</div>
```

## Step 2: Styling the stepper timeline
Next, let's add some CSS to style our stepper timeline. We'll use flexbox to align the steps horizontally and add some basic styling.

```css
#stepper {
  display: flex;
  justify-content: space-between;
}

.step {
  padding: 10px;
  border: 1px solid #ccc;
}

.step.active {
  background-color: #ccc;
}
```

## Step 3: Making the stepper responsive
Now, we want our stepper timeline to be responsive, meaning it should adapt to different screen sizes. We can achieve this using `MediaQuery` in CSS.

```css
/* Default styles */
#stepper {
  display: flex;
  justify-content: space-between;
}

.step {
  padding: 10px;
  border: 1px solid #ccc;
}

.step.active {
  background-color: #ccc;
}

/* Media Query for smaller screens */
@media (max-width: 600px) {
  #stepper {
    flex-direction: column;
  }

  .step {
    margin-bottom: 10px;
  }
}
```

In the above code, we have added a media query that targets screens with a maximum width of 600 pixels. Inside this media query, we change the direction of the flex container to `column`, which causes the steps to stack vertically. Additionally, we add some bottom margin to the steps to provide spacing between them.

## Conclusion
By using `MediaQuery` in CSS, we can easily create a responsive stepper timeline that adapts to different screen sizes. This allows for a better user experience on both desktop and mobile devices.

#webdevelopment #responsivedesign