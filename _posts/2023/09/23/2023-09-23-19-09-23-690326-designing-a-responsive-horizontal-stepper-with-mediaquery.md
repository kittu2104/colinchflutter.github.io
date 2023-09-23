---
layout: post
title: "Designing a responsive horizontal stepper with `MediaQuery`"
description: " "
date: 2023-09-23
tags: [f2f2f2, WebDevelopment, ResponsiveDesign]
comments: true
share: true
---

In web development, **responsive design** plays a crucial role in creating websites that can adapt to various screen sizes. A common UI pattern seen in many web applications is the **stepper** or **wizard**, which allows users to progress through a sequence of steps or actions.

In this blog post, we will explore how to design a **responsive horizontal stepper** using `MediaQuery` in a web application. We will demonstrate using the popular programming language **JavaScript** and the **React** library.

## Setting up the Project

To get started, we need to set up our project with the necessary tools and dependencies. Assuming you have Node.js and npm (Node Package Manager) installed, you can follow these steps:

1. Create a new directory for your project.
2. Open the command line or terminal and navigate to the project directory.
3. Run `npx create-react-app responsive-stepper` to set up a new React project.
4. Once the installation is complete, navigate into the project directory with `cd responsive-stepper`.
5. Open the project in your preferred code editor.

## Implementing the Stepper Component

In the `src` directory of your React project, create a new file called `Stepper.js`. We will define our stepper component in this file. Here's an example implementation to get started:

```javascript
import React from 'react';
import { useMediaQuery } from 'react-responsive';

const Stepper = () => {
  const isMobile = useMediaQuery({ query: '(max-width: 767px)' });

  return (
    <div className="stepper">
      <div className="step">Step 1</div>
      <div className="step">Step 2</div>
      <div className="step">Step 3</div>
      <div className="step">Step 4</div>
    </div>
  );
};

export default Stepper;
```

In the code above, we import the `useMediaQuery` hook from the `react-responsive` library. This hook allows us to check the screen size and conditionally render the stepper horizontally or vertically based on the media query.

Inside the `Stepper` component, we use the `useMediaQuery` hook to determine if the screen width is less than or equal to 767 pixels, which would indicate a mobile device. We store the result in the `isMobile` variable.

Next, we return a `div` element with class `stepper` and four `div` elements with class `step`, representing the individual steps of the stepper.

## Styling the Stepper

To style the stepper, we can create a new file called `Stepper.css` in the same directory as `Stepper.js`. Add the following CSS code to style the stepper:

```css
.stepper {
  display: flex;
  flex-direction: ${isMobile ? 'column' : 'row'};
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #f2f2f2;
  border-radius: 5px;
}

.step {
  width: 100px;
  height: 50px;
  background-color: #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
}
```

The CSS code above styles the `stepper` class with a flex container that arranges the steps either in a column or row based on the `isMobile` value. The `step` class represents each individual step and sets the width, height, background color, and other styling properties.

## Using the Stepper Component

To use the `Stepper` component in your React application, open the `src/App.js` file and update its contents as follows:

```javascript
import React from 'react';
import Stepper from './Stepper';
import './App.css';

function App() {
  return (
    <div className="App">
      <Stepper />
    </div>
  );
}

export default App;
```

Here, we import the `Stepper` component and include it within the `App` component. Save the file and run the React development server with `npm start` to see the responsive horizontal stepper in action.

## Conclusion

By utilizing the `MediaQuery` `useMediaQuery` hook from `react-responsive` library, we have successfully designed a responsive horizontal stepper in a React application. This technique allows the stepper to adapt to different screen sizes, providing an optimal user experience across devices.

Remember that this is just a basic example of a responsive stepper, and you can extend it further by adding functionality to move between steps, highlight the active step, and incorporate user interactions.

#WebDevelopment #ResponsiveDesign