---
layout: post
title: "Designing a responsive loading spinner with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [WebDevelopment, ResponsiveDesign]
comments: true
share: true
---

In today's digital age, where websites and applications frequently make asynchronous requests and load content dynamically, it's important to provide users with a visual indication that the system is still working. One popular way to do this is by using a loading spinner, which rotates to give the user a sense of progress. In this blog post, we will explore how to design a responsive loading spinner using `MediaQuery` in CSS.

## Step 1: HTML Markup

First, let's start by creating the HTML markup for our loading spinner. We will use a `<div>` element with a class name of "spinner".

```html
<div class="spinner"></div>
```

## Step 2: CSS Styling

Next, let's style the loading spinner using CSS. We'll use a combination of Flexbox and CSS animations to create the desired effect. Here's an example CSS code for the spinner:

```css
.spinner {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.spinner::before {
  content: "";
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 4px solid #ccc;
  border-top-color: #333;
  animation: spin 1s infinite linear;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

In the above code, we set `display: flex;` to center the spinner vertically and horizontally within its container. Then, we use the `::before` pseudo-element to create a circular shape for the spinner using `border-radius` and set the border colors for a nice contrast. Finally, we apply an animation named "spin" to the spinner, which rotates it continuously using the `transform: rotate()` property.

## Step 3: Responsive Design with `MediaQuery`

To make our loading spinner responsive, we can utilize `MediaQuery` to adjust its size and position based on the screen size. Here's an example of how we can modify the CSS code to make it responsive:

```css
@media (max-width: 768px) {
  .spinner {
    height: 50vh;
  }

  .spinner::before {
    width: 20px;
    height: 20px;
    border-width: 2px;
  }
}
```

In the code above, we use a `max-width` media query to target screens with a maximum width of 768 pixels. Within this media query, we adjust the height of the spinner to 50% of the viewport height and reduce the size of the spinner's border and dimensions.

## Conclusion

By combining the power of CSS animations, Flexbox, and `MediaQuery`, we can easily create a responsive loading spinner that adapts to different screen sizes. This helps provide a seamless user experience and lets users know that the system is still working in the background.

Remember to experiment with different styles, colors, and animations to match your application's design and branding. With a little creativity, you can transform a basic loading spinner into an eye-catching element that engages users while they wait.

#WebDevelopment #CSS #ResponsiveDesign