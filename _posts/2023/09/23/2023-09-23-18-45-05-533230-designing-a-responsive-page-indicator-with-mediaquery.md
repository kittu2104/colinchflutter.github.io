---
layout: post
title: "Designing a responsive page indicator with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [ff0000, webdesign, responsivedesign]
comments: true
share: true
---

A page indicator is a visual element that shows the progress or current position of a user within a series of pages or sections. It helps users navigate through the content and provides them with a sense of orientation. By making the page indicator responsive, we ensure a consistent user experience across different devices and screen sizes.

Here's an example of how we can implement a responsive page indicator using `MediaQuery` in HTML, CSS, and JavaScript:

## HTML
```html
<div class="page-indicator">
  <span class="dot"></span>
  <span class="dot"></span>
  <span class="dot"></span>
</div>
```

## CSS
```css
.page-indicator {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #ccc;
  margin: 0 5px;
  transition: background-color 0.3s ease-in-out;
}

.active-dot {
  background-color: #ff0000;
}
```

## JavaScript
```javascript
const dots = document.querySelectorAll('.dot');
const sections = document.querySelectorAll('section');

window.addEventListener('scroll', () => {
  let currentSection = '';

  sections.forEach((section) => {
    const sectionTop = section.offsetTop;
    const sectionHeight = section.clientHeight;

    if (window.pageYOffset >= sectionTop - sectionHeight / 2) {
      currentSection = section.getAttribute('id');
    }
  });

  dots.forEach((dot) => {
    dot.classList.remove('active-dot');
    if (dot.id === currentSection) {
      dot.classList.add('active-dot');
    }
  });
});
```

In the above code, we have an HTML structure with a `<div>` element containing multiple `<span>` elements representing the dots in the page indicator. CSS is used to style the dots and provide transitions. JavaScript is used to listen to the scroll event and determine which section is currently in view. The active dot is highlighted by adding the `active-dot` class.

To make the page indicator responsive, you can use `@media` queries in CSS to modify the styling based on different screen sizes. For example, you can change the dot size or spacing between dots for smaller screens.

With this responsive page indicator, users will have a clear visual indication of their progress through the pages or sections of your web application, improving the overall user experience.

#webdesign #responsivedesign