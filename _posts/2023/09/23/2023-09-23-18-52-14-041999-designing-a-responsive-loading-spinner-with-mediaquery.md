---
layout: post
title: "Designing a responsive loading spinner with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [webdevelopment, responsivedesign]
comments: true
share: true
---

As users navigate websites or use web applications, it's important to provide feedback on the loading process to keep them engaged and informed. One popular way to accomplish this is by using a loading spinner. In this tutorial, we'll explore how to design a responsive loading spinner using `MediaQuery`.

## What is MediaQuery?

`MediaQuery` is a feature in CSS that allows us to apply different styles based on the viewport size or device characteristics. By using `MediaQuery`, we can make our loading spinner adapt to different screen sizes and provide a seamless experience for all users.

## Step 1: HTML Markup

First, let's set up the HTML markup for our loading spinner:

```html
<div class="loading-spinner">
   <div class="spinner"></div>
</div>
```

We wrap our spinner in a container div with the class `loading-spinner`. This container will help us center the spinner on the page.

## Step 2: CSS Styling

Next, let's add some CSS styles to create the spinning effect for our loading spinner:

```css
.loading-spinner {
   display: flex;
   align-items: center;
   justify-content: center;
   height: 100vh;
}

.spinner {
   width: 50px;
   height: 50px;
   border: 5px solid #ccc;
   border-top-color: #000;
   border-radius: 50%;
   animation: spin 1s infinite linear;
}

@keyframes spin {
   0% {
       transform: rotate(0);
   }
   100% {
       transform: rotate(360deg);
   }
}
```

In the `.loading-spinner` class, we set `display` to `flex` and use `align-items` and `justify-content` to center the spinner vertically and horizontally within the container.

In the `.spinner` class, we set the width, height, and border properties to define the size and appearance of the spinner. We use `border-top-color` to change the color of the top border, creating a visually appealing effect. Finally, we define an animation called `spin` that rotates the spinner 360 degrees infinitely in a linear motion.

## Step 3: Responsive Design with MediaQuery

Now that we have our basic loading spinner, let's make it responsive using `MediaQuery`. We'll update the styles for different viewport sizes.

```css
@media screen and (max-width: 600px) {
   .spinner {
      width: 30px;
      height: 30px;
      border-width: 3px;
   }
}

@media screen and (min-width: 601px) and (max-width: 1200px) {
   .spinner {
      width: 40px;
      height: 40px;
      border-width: 4px;
   }
}
```

In this example, we define two `MediaQuery` rules. The first rule targets screens with a maximum width of 600 pixels and adjusts the size of the spinner to 30px by 30px, with a thinner border.

The second rule targets screens with a width between 601 pixels and 1200 pixels and adjusts the size of the spinner to 40px by 40px, with a slightly thicker border.

Feel free to adjust the sizes and borders in the `MediaQuery` rules to fit your desired responsive design.

## Conclusion

By using `MediaQuery`, we can create a responsive loading spinner that adapts to different screen sizes. This ensures that the spinner remains visually appealing and functional across various devices and viewport sizes. 

Remember to test your spinner on different devices and screen sizes to ensure it looks and behaves as expected. Happy spinning!

#webdevelopment #responsivedesign