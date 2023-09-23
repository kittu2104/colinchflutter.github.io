---
layout: post
title: "Building a responsive image gallery with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [webdevelopment, responsivegallery]
comments: true
share: true
---

In this tutorial, we will be building a responsive image gallery using the `MediaQuery` API. The `MediaQuery` API allows us to apply different styles to our webpage based on the user's device or screen size. By utilizing this API, we can create a gallery that adapts to different screen sizes, providing a better user experience across devices.

## Step 1: Setup

First, let's start by creating the basic HTML structure for our image gallery.

```html
<div class="gallery">
  <img src="image1.jpg" alt="Image 1" />
  <img src="image2.jpg" alt="Image 2" />
  <img src="image3.jpg" alt="Image 3" />
  <!-- Add more images as needed -->
</div>
```

## Step 2: Add CSS

Next, we'll add some CSS styles to make our image gallery responsive.

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 10px;
}

.gallery img {
  width: 100%;
  height: auto;
}
```

In the above CSS code, we use the `grid` layout to create a responsive grid of images. The `grid-template-columns` property ensures that the images will wrap to a new row when the screen size is too small to fit in the specified width. The `gap` property adds a small gap between the images, giving them some breathing room.

## Step 3: Applying MediaQuery

Now, let's make the image gallery adapt dynamically to different screen sizes. We'll use the `MediaQuery` API to apply different styles for smaller screens.

```css
@media (max-width: 600px) {
  .gallery {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  }
}
```

In the above code, we define a media query using `(max-width: 600px)`, which means the styles within this media query will only apply when the screen width is less than or equal to 600 pixels. In this case, we modify the `grid-template-columns` property to make the images smaller and allow more images to fit in a row.

## Step 4: Testing

To test our responsive image gallery, simply resize your browser window or use device emulation tools in your browser's developer tools. You should see the images adapt and reflow to fit the available space based on the screen size.

# Conclusion

In this tutorial, we learned how to build a responsive image gallery using the `MediaQuery` API. With this API, we can create versatile webpages that adapt and provide a smooth user experience on various devices and screen sizes. Utilizing media queries and the `grid` layout, we can easily build responsive image galleries and other interactive components.

#webdevelopment #responsivegallery