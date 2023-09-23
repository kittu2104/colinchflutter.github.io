---
layout: post
title: "Designing a responsive toggle switch with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [2196f3]
comments: true
share: true
---

In today's fast-paced world, creating responsive designs has become crucial. One key element of responsive design is creating toggle switches that adapt to different screen sizes. In this tutorial, we will discuss how to create a responsive toggle switch using `MediaQuery` in CSS.

## What is MediaQuery?

The `MediaQuery` is a CSS feature that allows you to apply different styles based on the characteristics of the device or viewport. By using `MediaQuery`, you can easily create responsive designs that adapt to different screen sizes and orientations.

## Creating the HTML structure

Let's start by creating the HTML structure for our toggle switch:

```html
<div class="toggle-switch">
  <input type="checkbox" id="toggle" class="checkbox">
  <label for="toggle" class="toggle-slider"></label>
</div>
```

In this code snippet, we have a `div` element with the class `.toggle-switch`. Inside the `div`, we have an `input` element of type checkbox with the id `toggle` and the class `.checkbox`. Following the `input` element, we have a `label` element with the class `.toggle-slider`.

## Styling the Toggle Switch

Now, let's style our toggle switch using CSS:

```css
.toggle-switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.checkbox {
  display: none;
}

.toggle-slider {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  border-radius: 34px;
  transition: background-color 0.4s;
}

.toggle-slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: #fff;
  border-radius: 50%;
  transition: transform 0.4s;
}

.checkbox:checked + .toggle-slider {
  background-color: #2196f3;
}

.checkbox:checked + .toggle-slider:before {
  transform: translateX(26px);
}
```

In this CSS code, we style the `.toggle-switch` as a container for our toggle switch. The `.checkbox` class is used to hide the checkbox input element. The `.toggle-slider` class represents the actual toggle switch. 

We use `MediaQuery` to apply different styles based on screen size and orientation. For example, you can add the following `MediaQuery` to make the toggle switch smaller on mobile devices:

```css
@media screen and (max-width: 600px) {
  .toggle-switch {
    width: 40px;
    height: 24px;
  }
}
```

By using `MediaQuery`, you have the flexibility to adapt the toggle switch to different screen sizes, ensuring a seamless user experience across devices.

## Conclusion

In this tutorial, we explored how to create a responsive toggle switch using `MediaQuery` in CSS. `MediaQuery` allows you to apply different styles based on the characteristics of the device or viewport, making it easy to create responsive designs that adapt to different screen sizes and orientations.