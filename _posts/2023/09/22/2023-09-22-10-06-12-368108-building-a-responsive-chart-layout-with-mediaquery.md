---
layout: post
title: "Building a responsive chart layout with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [chartContainer, chartContainer]
comments: true
share: true
---

In today's world, where the majority of people access the internet using different devices with varying screen sizes, it's crucial to make sure your website or application is responsive. One common challenge developers face while building responsive layouts is accommodating complex components like charts. In this article, we'll explore how to build a responsive chart layout using `MediaQuery` in your web application.

## What is MediaQuery?

`MediaQuery` is a powerful feature in CSS that allows you to apply different styles based on the characteristics of the device or browser being used to view your web app. With `MediaQuery`, you can target specific screen sizes, resolutions, orientations, and more.

## Setting up the Chart Component

To begin, let's assume that you already have a basic chart component in your web application. For this example, we'll use a simple line chart using a popular charting library called [Chart.js](https://www.chartjs.org/). The first step is to create a container element for the chart:

```html
<div id="chartContainer">
  <canvas id="chart"></canvas>
</div>
```

The chart will be rendered inside the `canvas` element within the `chartContainer` div.

## Applying Responsive Styles

Now that we have our chart container set up, we can start applying responsive styles using `MediaQuery`. We want the chart to display differently depending on the screen size. Let's say we want the chart to take up the full width of the screen on smaller devices (e.g., mobile phones) but only occupy half of the screen on larger devices (e.g., tablets or desktops).

```css
#chartContainer {
  height: 300px;
  width: 100%;
}

@media (min-width: 768px) {
  #chartContainer {
    width: 50%;
  }
}
```

Here, we set the `height` of the `chartContainer` to 300 pixels and set the `width` to `100%` initially. Then, we use `@media` to apply styles only when the screen width is greater or equal to 768 pixels. In this case, we set the `width` of the `chartContainer` to 50%.

## Updating Chart Size on Window Resize

While the above approach works for different screen sizes, we also need to handle the scenario when the user resizes the browser window. We want the chart to update dynamically based on the new screen size. This can be achieved by listening for the `resize` event and updating the chart dimensions accordingly.

```javascript
window.addEventListener('resize', function() {
  var chartContainer = document.getElementById('chartContainer');
  var chartCanvas = document.getElementById('chart');

  chartContainer.style.width = '100%';
  setTimeout(function() {
    chartCanvas.width = chartContainer.offsetWidth;
    chartCanvas.height = chartContainer.offsetWidth;
  }, 0);
});
```

In this JavaScript snippet, we add a `resize` event listener to the `window` object in order to detect when the window is resized. Within the event handler, we get references to the chart container and canvas elements. Then, we dynamically update the `width` and `height` of the chart canvas to match the updated dimensions of the container.

## Conclusion

In this article, we explored how to build a responsive chart layout using `MediaQuery` in your web application. By applying different styles depending on the screen size using `MediaQuery`, and dynamically updating the chart dimensions on window resize, we ensure that our charts are visually appealing and usable across devices. By making your charts responsive, you can provide a seamless and engaging experience to your users, regardless of the device they're using.

#tech #webdevelopment