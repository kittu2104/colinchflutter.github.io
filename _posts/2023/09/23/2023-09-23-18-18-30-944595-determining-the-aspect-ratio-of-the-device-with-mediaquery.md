---
layout: post
title: "Determining the aspect ratio of the device with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [AspectRatio, MediaQuery]
comments: true
share: true
---

With `MediaQuery`, developers can easily apply specific styles or perform certain actions based on the dimensions of the viewport. To determine the aspect ratio, we can use the `aspect-ratio` feature of `MediaQuery`.

Let's take a look at an example of how to use `MediaQuery` to determine the aspect ratio of a device:

```javascript
if (window.matchMedia("(aspect-ratio: 16/9)").matches) {
    console.log("The device has a 16:9 aspect ratio.");
} else if (window.matchMedia("(aspect-ratio: 4/3)").matches) {
    console.log("The device has a 4:3 aspect ratio.");
} else {
    console.log("The device has a different aspect ratio.");
}
```

In the above code snippet, we first check if the device has a 16:9 aspect ratio using `window.matchMedia("(aspect-ratio: 16/9)")`. If the condition is true, we log a message to the console indicating that the device has a 16:9 aspect ratio. If not, we proceed to the next condition and check if the aspect ratio is 4:3. Finally, if none of the conditions match, we assume that the device has a different aspect ratio.

Remember to include this code within an event listener or a `window.onresize` callback to ensure that it is executed whenever the viewport dimensions change.

By utilizing `MediaQuery` and the `aspect-ratio` feature, developers can determine the aspect ratio of the user's device, enabling them to create responsive layouts that adapt to different screen sizes and orientations.

#AspectRatio #MediaQuery