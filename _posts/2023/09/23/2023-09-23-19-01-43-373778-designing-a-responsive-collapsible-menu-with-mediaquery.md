---
layout: post
title: "Designing a responsive collapsible menu with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [menu, menu, menu, menu, menu, menu, menu, webdesign, responsivedesign]
comments: true
share: true
---

In this article, we will learn how to create a responsive collapsible menu using `MediaQuery` in CSS. Responsive web design is crucial for delivering a consistent user experience across different devices and screen sizes. With `MediaQuery`, we can define CSS rules that are applied based on the user's device or viewport size.

## HTML Structure

Let's start by defining the HTML structure for our collapsible menu. We will use a `<nav>` element with an unordered list `<ul>` for the menu items. Each menu item will be represented by a `<li>` element.

```html
<nav id="menu">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

## CSS Styles

Next, we will define the CSS styles for our menu. We will make use of `MediaQuery` to apply different styles for different screen sizes.

```css
/* Default styles for the menu */
#menu ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
#menu li {
  display: inline-block;
  margin-right: 20px;
}
#menu li a {
  text-decoration: none;
}

/* Media query for screen sizes up to 768px */
@media only screen and (max-width: 768px) {
  #menu li {
    display: block;
    margin-right: 0;
  }
}
```

In the above code, we define the default styles for the menu using the `#menu`, `#menu ul`, and `#menu li` selectors. Then, we define a media query using `@media` to target screen sizes up to 768px. Inside the media query, we change the `display` property of the menu items to `block` to make them stack vertically.

## JavaScript Functionality

Finally, we will add JavaScript functionality to make the menu collapsible. We will toggle a CSS class `active` on the `<nav>` element when the menu button is clicked.

```javascript
const menuButton = document.getElementById('menu-button');
const menu = document.getElementById('menu');

menuButton.addEventListener('click', () => {
  menu.classList.toggle('active');
});
```

In the above code, we select the menu button and the menu element using their respective `id` attributes. Then, we add a click event listener to the menu button and toggle the `active` class on the menu element when clicked.

## Conclusion

By using `MediaQuery`, we can easily create a responsive collapsible menu that adapts to different screen sizes. This allows us to provide an optimal user experience on both desktop and mobile devices. Remember to test your menu on various devices and adjust the `MediaQuery` breakpoints as needed.

#webdesign #responsivedesign