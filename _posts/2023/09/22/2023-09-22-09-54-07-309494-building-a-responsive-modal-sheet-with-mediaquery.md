---
layout: post
title: "Building a responsive modal sheet with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [WebDevelopment, ResponsiveDesign]
comments: true
share: true
---

## What is `MediaQuery`?

`MediaQuery` is a Javascript API that allows us to dynamically query and listen for changes in the browser's viewport or device characteristics. It provides a way to conditionally apply styles or behavior based on the current display environment.

## Creating the Modal Sheet

To start, let's create the basic structure of our modal sheet using HTML and CSS:

```html
<div class="modal-overlay">
  <div class="modal-content">
    <!-- content goes here -->
  </div>
</div>
```

```css
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: none;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
}
```

By default, we set the `display` property of the overlay to `none` so that it is hidden initially. We will use `MediaQuery` to control when it should be displayed.

## Making it Responsive

Using `MediaQuery`, we can detect changes in the viewport width and adjust the appearance of our modal sheet accordingly. Let's add the following JavaScript code:

```javascript
const modalOverlay = document.querySelector('.modal-overlay');

const mediaQuery = window.matchMedia('(max-width: 768px)');

function handleMediaQueryChange(event) {
  if (event.matches) {
    modalOverlay.style.display = 'flex';
  } else {
    modalOverlay.style.display = 'none';
  }
}

// Add event listener to the media query
mediaQuery.addEventListener('change', handleMediaQueryChange);

// Initial check
handleMediaQueryChange(mediaQuery);
```

In the above code, we select the `.modal-overlay` element using `querySelector()` and define a `mediaQuery` variable with a maximum width of 768 pixels. We then define a callback function `handleMediaQueryChange()` that will be triggered whenever the media query matches or unmatches.

Inside the callback function, we update the `display` property of the modal overlay based on the media query match. If the media query is matched (viewport width is less than or equal to 768 pixels), we set the display property to `flex` so that the modal sheet is visible. Otherwise, we set it to `none` to hide the sheet.

Finally, we add an event listener to the media query using `addEventListener()` to listen for changes and call the `handleMediaQueryChange()` function. We also call the `handleMediaQueryChange()` function initially to check the initial state.

## Conclusion

In this blog post, we learned how to create a responsive modal sheet using `MediaQuery`. By leveraging the power of `MediaQuery`, we were able to dynamically adjust the appearance of our modal sheet based on the user's viewport size. This helps in providing a seamless and user-friendly experience across different devices and screen sizes.

#WebDevelopment #ResponsiveDesign