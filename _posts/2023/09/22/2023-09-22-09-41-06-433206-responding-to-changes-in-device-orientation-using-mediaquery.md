---
layout: post
title: "Responding to changes in device orientation using `MediaQuery`"
description: " "
date: 2023-09-22
tags: [responsive, deviceorientation]
comments: true
share: true
---

Fortunately, handling device orientation changes in your web application is relatively straightforward using the `MediaQuery` API in CSS. This API allows you to query various characteristics of the user's device, including orientation.

To respond to changes in device orientation, you can use the `@media` rule in CSS along with the `orientation` media feature. The `orientation` feature can have two values: `portrait` or `landscape`, depending on the current orientation of the device.

Here is an example of using `MediaQuery` to style an element differently based on the device's orientation:

```css
@media (orientation: portrait) {
  .my-element {
    /* styles for portrait orientation */
    color: blue;
  }
}

@media (orientation: landscape) {
  .my-element {
    /* styles for landscape orientation */
    color: red;
  }
}
```

In the above example, the `.my-element` class will have different colors depending on whether the device is in portrait or landscape mode. You can customize the styles inside the respective media queries to fit your design requirements.

To take it a step further and dynamically handle device orientation changes in JavaScript, you can listen for the `change` event on the `window.matchMedia()` object. Here's an example:

```javascript
const handleOrientationChange = () => {
  if (window.matchMedia("(orientation: portrait)").matches) {
    // Handle portrait orientation
    console.log("Portrait mode");
  } else {
    // Handle landscape orientation
    console.log("Landscape mode");
  }
};

window.matchMedia("(orientation: portrait)").addListener(handleOrientationChange);
```

In the above JavaScript code, the `handleOrientationChange` function is called whenever there is a change in the device's orientation. You can then perform any necessary actions or updates based on the current orientation.

By utilizing `MediaQuery` and listening for orientation changes, you can create a responsive web application that adapts seamlessly to different device orientations. This ensures a smooth and user-friendly experience, regardless of how users hold or rotate their devices.

#responsive #deviceorientation