---
layout: post
title: "Building a responsive image gallery with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [ResponsiveDesign]
comments: true
share: true
---

In this tutorial, we will learn how to build a responsive image gallery using the `MediaQuery` class in CSS. 

![responsive-image-gallery](https://example.com/image-gallery.png)

## Introduction

A responsive image gallery is an essential component of any modern website. It allows users to view a collection of images in an organized and visually appealing manner. With the help of the `MediaQuery` class, we can easily create a gallery that adapts to different screen sizes and devices.

## Prerequisites

To follow along with this tutorial, you will need:

- Basic knowledge of HTML and CSS
- Text editor or an integrated development environment (IDE)
- A modern web browser

## Getting Started

Create a new HTML file and add the following code:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Responsive Image Gallery</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <div class="image-gallery">
      <img src="image1.jpg">
      <img src="image2.jpg">
      <img src="image3.jpg">
    </div>
  </body>
</html>
```

In the above code, we have a basic HTML structure with a `div` element that will contain our image gallery. We have also added a link to an external CSS file called "styles.css" for styling purposes.

## Styling the Image Gallery

Now, let's create the CSS file and add the necessary styles:

```css
.image-gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}

@media (max-width: 767px) {
  .image-gallery {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 479px) {
  .image-gallery {
    grid-template-columns: 1fr;
  }
}
```

In the above code snippet, we defined the general styling for the image gallery as a CSS grid with three columns using `grid-template-columns`. We also set a gap of 10 pixels between the images using `grid-gap`.

For responsiveness, we used `@media` queries to change the number of columns based on different breakpoints. For screen sizes less than or equal to 767 pixels, the gallery will display two columns, and for screen sizes less than or equal to 479 pixels, it will display a single column.

## Conclusion

By utilizing the `MediaQuery` class in CSS, we can easily build a responsive image gallery that adjusts its layout based on the screen size or device being used. This allows for a more optimal user experience and ensures that our image gallery looks great on any device. 

Make sure to experiment and customize the style and layout of your image gallery to suit your specific needs!

**#ResponsiveDesign #CSS**