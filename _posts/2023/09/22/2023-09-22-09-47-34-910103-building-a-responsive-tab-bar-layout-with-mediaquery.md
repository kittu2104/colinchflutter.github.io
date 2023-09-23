---
layout: post
title: "Building a responsive tab bar layout with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [f2f2f2, react]
comments: true
share: true
---

In web development, creating a responsive user interface is essential to ensure compatibility across different devices and screen sizes. One common UI element is a tab bar, which allows users to navigate between different sections of a website or application.

In this tutorial, we will explore how to build a responsive tab bar layout using the `MediaQuery` class in **React**. The `MediaQuery` class allows us to conditionally render components based on the screen size or other media features.

Let's get started by setting up a basic React project with the necessary dependencies. 

## Step 1: Setup

First, create a new React project using `create-react-app`, and navigate to the project's directory in your terminal.

```bash
npx create-react-app tab-bar-layout
cd tab-bar-layout
```

Next, install the `styled-components` library, which we will use for styling our tab bar.

```bash
npm install styled-components
```

## Step 2: Creating the TabBar component

Inside the `src` directory, create a new file called `TabBar.js`. In this file, we will define our `TabBar` component.

```jsx
import React from 'react';
import styled from 'styled-components';

const TabBarWrapper = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f2f2;
`;

const TabBarItem = styled.div`
  padding: 10px;
  margin: 0 10px;
  font-size: 18px;
  cursor: pointer;

  ${({ active }) => active && `
    font-weight: bold;
  `}
`;

const TabBar = ({ tabs, activeTab, onChangeTab }) => {
  return (
    <TabBarWrapper>
      {tabs.map(tab => (
        <TabBarItem 
          key={tab.id}
          active={tab.id === activeTab}
          onClick={() => onChangeTab(tab.id)}
        >
          {tab.label}
        </TabBarItem>
      ))}
    </TabBarWrapper>
  );
};

export default TabBar;
```

In the above code, we have defined the `TabBarWrapper` and `TabBarItem` styled-components that will be used to style our tab bar. The `TabBar` component receives `tabs`, `activeTab`, and `onChangeTab` props to render the tabs and handle tab selection.

## Step 3: Adding media queries to the TabBar component

With our basic tab bar layout in place, we can now add media queries to make it responsive.

First, import the `MediaQuery` class from the `react-responsive` library. If you haven't installed it yet, run the following command:

```bash
npm install react-responsive
```

Next, wrap the `TabBar` component inside a `MediaQuery` component and define the desired breakpoints. In this example, we will use a breakpoint of 768 pixels to switch the tab bar to a vertical layout on smaller screens:

```jsx
import React from 'react';
import { MediaQuery } from 'react-responsive';
import TabBar from './TabBar';

const App = () => {
  const tabs = [
    { id: 'tab1', label: 'Tab 1' },
    { id: 'tab2', label: 'Tab 2' },
    { id: 'tab3', label: 'Tab 3' },
  ];
  const [activeTab, setActiveTab] = React.useState('tab1');

  const handleChangeTab = (tabId) => {
    setActiveTab(tabId);
  };

  return (
    <MediaQuery maxWidth={768}>
      {(matches) => (
        <TabBar
          tabs={tabs}
          activeTab={activeTab}
          onChangeTab={handleChangeTab}
          vertical={matches}
        />
      )}
    </MediaQuery>
  );
};

export default App;
```

In the code above, we pass the `vertical` prop to the `TabBar` component based on the `matches` value from the `MediaQuery` component. We can then use this prop to style the tab bar differently when it's in the vertical layout.

## Step 4: Styling the TabBar component

Feel free to style the `TabBar` component to match your design. Use CSS properties or additional styled-components to customize the appearance of the tab bar.

## Conclusion

In this tutorial, we've learned how to build a responsive tab bar layout using the `MediaQuery` class in React. By using media queries, we can conditionally render components and adjust the layout based on the screen size. This allows for a better user experience across different devices and screen sizes.

Remember to test your tab bar layout on various devices and screen sizes to ensure it's responsive and works as expected.

#react #webdevelopment