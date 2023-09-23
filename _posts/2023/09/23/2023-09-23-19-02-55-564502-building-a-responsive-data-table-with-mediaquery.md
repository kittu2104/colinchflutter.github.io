---
layout: post
title: "Building a responsive data table with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [WebDevelopment]
comments: true
share: true
---

When it comes to displaying data in a table format on a website, it's essential to ensure that the table is responsive and can adapt to different screen sizes. In this blog post, we will explore how to create a responsive data table using the `MediaQuery` feature in CSS.

## What is `MediaQuery`?

`MediaQuery` is a CSS feature that allows us to apply different styles based on different media types or conditions, such as screen size, screen resolution, device orientation, etc. By using `MediaQuery`, we can define specific styles for various devices or screen sizes, making our website adapt to different viewing environments.

## Building the Data Table

Let's assume we have a simple HTML table structure like this:

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th>Phone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>John Doe</td>
      <td>johndoe@example.com</td>
      <td>1234567890</td>
    </tr>
    <!-- More rows... -->
  </tbody>
</table>
```

To make our data table responsive, we can utilize `MediaQuery` in CSS to adjust the table layout based on different screen sizes.

## Applying `MediaQuery` Styles

We can define different styles for the table columns at different screen sizes by adding `MediaQuery` conditions in our CSS file. Let's consider an example where we want the table rows to stack vertically when the screen width is less than 600 pixels.

```css
/* Default table styles */

table {
  width: 100%;
}

/* Apply styles for screens less than 600px wide */
@media (max-width: 600px) {
  table {
    display: block;
  }
  
  tr {
    display: block;
    margin-bottom: 1rem;
  }
  
  td {
    display: block;
  }
}
```

In the above example, we set the table to `display: block` and the table rows (`tr`) and table data (`td`) to `display: block` as well when the screen width is less than 600 pixels. This causes the rows to stack vertically, creating a more mobile-friendly presentation of the table.

## Conclusion

With the help of `MediaQuery`, we can easily create a responsive data table that adapts to different screen sizes. By applying different styles based on screen conditions, we can ensure that our data remains accessible and readable on any device. The ability to display tabular data in a responsive manner improves the overall user experience and makes our website more functional and user-friendly.

#WebDevelopment #CSS