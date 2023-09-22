---
layout: post
title: "Designing a responsive toggle switch with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [2196F3]
comments: true
share: true
---

In this blog post, we will explore how to design a responsive toggle switch using the `MediaQuery` feature in CSS. This will allow the toggle switch to adapt to different screen sizes and provide a seamless user experience across devices.

## What is a Toggle Switch?

A toggle switch, also known as a toggle button or switch button, is a user interface element that allows users to switch between two states or options. It is commonly used in settings, preferences, or on/off scenarios.

## Designing the Toggle Switch

To design a responsive toggle switch, we will use HTML and CSS. Let's start by creating the HTML structure:

```html
<label for="toggle" class="toggle-switch">
  <input type="checkbox" id="toggle" class="toggle-input">
  <span class="toggle-slider"></span>
</label>
```

Here, we have a `label` element that wraps an `input` element and a `span` element. The `input` element with `type="checkbox"` represents the toggle switch, and the `span` element acts as the slider.

Now, let's style the toggle switch using CSS:

```css
.toggle-switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.toggle-input {
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
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.toggle-slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  border-radius: 50%;
  transition: transform 0.3s ease;
}

.toggle-input:checked + .toggle-slider {
  background-color: #2196F3;
}

.toggle-input:checked + .toggle-slider:before {
  transform: translateX(26px);
}
```

In the CSS code above, we set the dimensions and basic styles for the toggle switch. The `toggle-slider` acts as the background of the toggle switch, and the `toggle-slider:before` represents the button or handle of the toggle switch. We use CSS transitions to animate the button when it is toggled.

## Making the Toggle Switch Responsive

To make the toggle switch responsive, we can use CSS `MediaQuery`. Let's say we want the toggle switch to be larger on larger screens. We can add the following CSS inside a media query:

```css
@media screen and (min-width: 768px) {
  .toggle-switch {
    width: 80px;
    height: 46px;
  }
}
```

Here, we increase the width and height of the toggle switch for screens with a minimum width of 768px. You can adjust the values as per your design requirements.

## Conclusion

In this blog post, we learned how to design a responsive toggle switch using `MediaQuery` in CSS. By applying different styles based on screen sizes, we can create a toggle switch that adapts to various devices and offers an optimal user experience.