---
layout: post
title: "Building a responsive timeline widget with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [hashtags, ResponsiveTimeline, MediaQuery]
comments: true
share: true
---

In today's technology-driven world, creating responsive and interactive user interfaces has become essential. A timeline widget is a great way to showcase chronological events or progress in a visually appealing manner. In this blog post, we will learn how to build a responsive timeline widget using `MediaQuery` in **HTML**, **CSS**, and **JavaScript**.

## Prerequisites

To follow along with this tutorial, you should have a basic understanding of HTML, CSS, and JavaScript.

## Getting Started

Let's start by setting up the basic structure of our timeline widget in HTML.

```html
<div class="timeline">
  <div class="timeline-item">...</div>
  <div class="timeline-item">...</div>
  <!-- Add more timeline items here -->
</div>
```

In the above code snippet, we have defined a `<div>` with the class `timeline` that will contain all the timeline items. Each timeline item is represented by a `<div>` element with the class `timeline-item`.

## Styling the Timeline

Next, let's add some CSS to style our timeline widget. We will be using Flexbox to create the horizontal layout and `MediaQuery` for responsiveness.

```css
.timeline {
  display: flex;
  flex-direction: row;
  overflow-x: scroll;
}

.timeline-item {
  flex: 1;
  min-width: 300px;
  margin: 0 10px;
}

/* Add responsive styles for different screen sizes */
@media screen and (max-width: 768px) {
  .timeline-item {
    min-width: 200px;
  }
}

@media screen and (max-width: 480px) {
  .timeline-item {
    min-width: 150px;
  }
}
```

In the above code, we have set the `display` property of the `.timeline` class to `flex` and `flex-direction` to `row` to create a horizontal layout for our timeline. We have also added some spacing and width constraints to the `.timeline-item` class.

To make the timeline responsive, we have used `MediaQuery` to define different width constraints based on the screen size. In this example, we have set the minimum width of the timeline item to `200px` for screens up to `768px`, and `150px` for screens up to `480px`.

## Making the Timeline Interactive

We can enhance our timeline widget by adding some interactivity using JavaScript. Let's write a small script that will allow us to navigate through the timeline items using left and right arrow keys.

```javascript
const timelineItems = document.querySelectorAll('.timeline-item');
let currentItemIndex = 0;

document.addEventListener('keydown', (event) => {
  if (event.key === 'ArrowLeft' && currentItemIndex > 0) {
    currentItemIndex--;
  } else if (event.key === 'ArrowRight' && currentItemIndex < timelineItems.length - 1) {
    currentItemIndex++;
  }

  scrollToItem(currentItemIndex);
});

function scrollToItem(index) {
  const item = timelineItems[index];
  item.scrollIntoView({ behavior: 'smooth', block: 'center' });
}
```

In the JavaScript code above, we first select all the timeline items using the `querySelectorAll` method. We also define a variable `currentItemIndex` to keep track of the currently active item, which is initially set to `0`.

We then add an event listener to the `keydown` event, which captures the left and right arrow key presses. Depending on the key pressed and the current item index, we update the `currentItemIndex` variable accordingly.

The `scrollToItem` function is called to smoothly scroll the timeline to the current item using the `scrollIntoView` method.

## Conclusion

By combining HTML, CSS, and JavaScript, we have built a responsive timeline widget with interactivity. We learned how to use `MediaQuery` to make the timeline adapt to different screen sizes. We also added keyboard navigation to navigate through the timeline items.

Feel free to experiment with the code and customize it according to your specific requirements. Adding animations or additional features can further enhance the functionality and visual appeal of your timeline widget.

#hashtags: #ResponsiveTimeline #MediaQuery